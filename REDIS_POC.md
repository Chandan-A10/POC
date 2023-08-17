
# Redis Caching in a Nest.js Application




## Step 1:Installation

First install required packages in your nestjs application

```bash
  npm install @nestjs/cache-manager cache-manager cache-manager-redis-yet redis
```
In order to enable caching, import the ``CacheModule`` from ``@nestjs/cache-manager`` and redisStore from ``cache-manager-redis-yet``.
```bash
  import { CacheModule } from '@nestjs/cache-manager';
  import { redisStore } from 'cache-manager-redis-yet';
```
Note: Your redis server should be running at port specified (here :6379).
## Step 2: Configure Cache Store with Redis
In this step, we will configure the cache store of our Nest.js application to use Redis.

1. Open the ```app.module.ts``` file located in the src folder of your project.

2. In the ```@Module()``` decorator of your AppModule class, update the imports array to configure the cache store with Redis:

```bash
@Module({
  imports: [
    CacheModule.registerAsync({
      isGlobal: true,
      useFactory: async () => ({
        store: await redisStore({
          socket: {
            host: 'localhost' //Redis server host,
            port: 6379 //Redis server port ,
          },
        }),
      }),
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
```
Instead of using ```CacheModule.register``` we have used ```CacheModule.registerAsync``` to asynchronously pass in module options instead of passing them statically at compile time.

Also we have used ```redisStore``` function provided by ```cache-manager-redis-yet``` to configure our redis store , you can modify its options according to your need.

When you want to use ``CacheModule`` in other modules, you'll need to import it (as is standard with any Nest module). Alternatively, declare it as a global module by setting the options object's ``isGlobal`` property to true, as shown below. In that case, you will not need to import CacheModule in other modules once it's been loaded in the root module (e.g., AppModule).
```bash
  CacheModule.register({
    isGlobal: true,
  });
```
## Step 3: Using cache module in your services
1. To interact with the cache manager instance, inject it to your class using the ```CACHE_MANAGER``` token, as follows:
```bash
  constructor( @Inject( CACHE_MANAGER ) private cacheManager: Cache) {}
```
2. The ```Cache``` class is imported from the ````cache-manager````, while ````CACHE_MANAGER```` token from the ````@nestjs/cache-manager package````.

3. To add an item to the cache, use the ``set`` method:
```bash
  await this.cacheManager.set('key', 'value');
```
You can manually specify a TTL (expiration time in milliseconds) for a specific key, as follows: 
```bash
  await this.cacheManager.set('key', 'value', 10000) //setting ttl value to 0 will disable expiration;
```
4. To get an item from the cache, use the ``get`` method:
```bash
  await this.cacheManager.get('key') //returns undefined if key doesn't exists;
```
5. To delete an item from the cache, use the ``del`` method:
```bash
  this.cacheManager.del('key');
```
6. To delete all the items from the cache, use the ``reset`` method:
```bash
  this.cacheManager.reset() //Note: this will empty the whole catchstore;
```
## Step:4 Auto-Caching a Controllers GET requests
To enable auto-caching responses, just tie the ``CacheInterceptor`` where you want to cache data.
```bash
//required imports
import { UseInterceptors } from '@nestjs/common';
import { CacheInterceptor } from '@nestjs/cache-manager';

@Controller()

//this will automatically cahe all of your Controller GET requests 
@UseInterceptors(CacheInterceptor)

export class AppController {
  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```
## Step:5 Overriding global cache properties
While global cache is enabled, cache entries are stored under a CacheKey that is auto-generated based on the route path. You may override certain cache settings (@CacheKey() and @CacheTTL()) on a per-method basis, allowing customized caching strategies for individual controller methods.

```bash
@Controller()
export class AppController {

  @CacheKey('custom_key')   //creating a custom key to store the cached data
  @CacheTTL(20)             //modifying ttl for this GET request
  async getHello() {
    return this.appService.getHello();
  }
}

```
