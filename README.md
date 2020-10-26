# job

Run on it's own goroutine

```golang
go myjob.Run()
```

Pass to a worker pool (we recommend [workerpool](https://github.com/gammazero/workerpool))

```golang
import "github.com/gammazero/workerpool"
wp := workerpool.New(10) // 10 workers max for N jobs
wp.Submit(myjob.Run) // myjob.Run is a `func()`
```