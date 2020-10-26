# job

 - Example
 
 See test file for detailed code
 
 ```golang
 import "github.com/oze4/job"
 
 func main() {
     resultsChan := make(chan job.Result)
     var results []job.Result
     
     somejob := job.NewJob("SomeJob", resultsChan, func() (interface{}, error) {
         time.Sleep(time.Second) // do something
         return someResult, orSomeError
     })
     
     //// Invoke "manually"
     go somejob.Run()
     
     //// or pass to workerpool
     // wp.Submit(somejob.Run) // github.com/gammazero/workerpool
     
     // somejob.Run is just a `func()`
     
     select {
     case r := <-results:
         results = append(results, r)
     }
     // do something with results
 }
 ```

 - Run on it's own goroutine

```golang
go myjob.Run()
```

 - Pass to a worker pool (we recommend [workerpool](https://github.com/gammazero/workerpool))

```golang
import "github.com/gammazero/workerpool"
wp := workerpool.New(10) // 10 workers max for N jobs
wp.Submit(myjob.Run) // myjob.Run is a `func()`
```
