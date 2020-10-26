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
