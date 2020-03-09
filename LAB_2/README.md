# Лабораторная работа №2 
### Знакомство с nginx
#### 1. Замерьте скорость отдачи контента на сервере из лабораторной работы №1 (отдача страниц, картинки, запросов к api). Добавьте логирование приходящих запросов.

##### Количество запросов 10, количество конкурентных запросов 100.
###### GET main page:
```
$ ab -c 10 -n 100 http://localhost:8080/
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient).....done


Server Software:        
Server Hostname:        localhost
Server Port:            8080

Document Path:          /
Document Length:        625 bytes

Concurrency Level:      10
Time taken for tests:   0.176 seconds
Complete requests:      100
Failed requests:        0
Total transferred:      91300 bytes
HTML transferred:       62500 bytes
Requests per second:    567.29 [#/sec] (mean)
Time per request:       17.628 [ms] (mean)
Time per request:       1.763 [ms] (mean, across all concurrent requests)
Transfer rate:          505.80 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       1
Processing:    10   14   4.2     13      40
Waiting:        7   11   4.1     10      37
Total:         10   14   4.1     13      40

Percentage of the requests served within a certain time (ms)
  50%     13
  66%     14
  75%     14
  80%     16
  90%     22
  95%     22
  98%     23
  99%     40
 100%     40 (longest request)
```
###### Logger:
```
{"time":"2020-03-08T19:14:29.303Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.311Z","lvl":"INFO","msg":"Response with status 200 in 9 ms."}
{"time":"2020-03-08T19:14:29.320Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.320Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.321Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.321Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.322Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.322Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.323Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.323Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.324Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.324Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.327Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.328Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.329Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.330Z","lvl":"INFO","msg":"Response with status 200 in 9 ms."}
{"time":"2020-03-08T19:14:29.331Z","lvl":"INFO","msg":"Response with status 200 in 9 ms."}
{"time":"2020-03-08T19:14:29.332Z","lvl":"INFO","msg":"Response with status 200 in 10 ms."}
{"time":"2020-03-08T19:14:29.333Z","lvl":"INFO","msg":"Response with status 200 in 10 ms."}
{"time":"2020-03-08T19:14:29.333Z","lvl":"INFO","msg":"Response with status 200 in 10 ms."}
{"time":"2020-03-08T19:14:29.334Z","lvl":"INFO","msg":"Response with status 200 in 11 ms."}
{"time":"2020-03-08T19:14:29.336Z","lvl":"INFO","msg":"Response with status 200 in 12 ms."}
{"time":"2020-03-08T19:14:29.339Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.339Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.340Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.340Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.340Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.341Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.341Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.342Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.342Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.346Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.346Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.347Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.347Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.348Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.348Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.349Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.349Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.350Z","lvl":"INFO","msg":"Response with status 200 in 9 ms."}
{"time":"2020-03-08T19:14:29.350Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.352Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.353Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.354Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.354Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.354Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.354Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.355Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.355Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.355Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.356Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.358Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.359Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.359Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.360Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.361Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.361Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.362Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.362Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.363Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.364Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.366Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.367Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.368Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.368Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.369Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.369Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.369Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.370Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.370Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.370Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.373Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.374Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.374Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.375Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.375Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.376Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.376Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.377Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.377Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.379Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.380Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.380Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.381Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.381Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.381Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.381Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.382Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.382Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.382Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.385Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.385Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.386Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.386Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.387Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.387Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.388Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.389Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.389Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.390Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.392Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.393Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.393Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.393Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.394Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.394Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.395Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.395Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.395Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.396Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.399Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.399Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.400Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.401Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.401Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.401Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.402Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.402Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.403Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:14:29.403Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.406Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.406Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.407Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.407Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.407Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.408Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.408Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.408Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.409Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.409Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.412Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.412Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.413Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.413Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.413Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.414Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.414Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.415Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.415Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.416Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.418Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.419Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.419Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.419Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.420Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.420Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.420Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.420Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.421Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.421Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.423Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.424Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.424Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.425Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.425Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.426Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.427Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.427Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.428Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.428Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.431Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.431Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.431Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.432Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.432Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.432Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.432Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.433Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.433Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.433Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.435Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:14:29.436Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.436Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.437Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.437Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.438Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.438Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.439Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.439Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.440Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:14:29.442Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.442Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.442Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.443Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.443Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.443Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.444Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.444Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.444Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.446Z","lvl":"INFO","msg":"Request from ::1: GET /"}
{"time":"2020-03-08T19:14:29.447Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.447Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.447Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.448Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.448Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.449Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.449Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:14:29.450Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.450Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:14:29.452Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
```
###### api GET:
```
$ ab -c 10 -n 100 http://localhost:8080/data
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient).....done


Server Software:        
Server Hostname:        localhost
Server Port:            8080

Document Path:          /data
Document Length:        81 bytes

Concurrency Level:      10
Time taken for tests:   0.119 seconds
Complete requests:      100
Failed requests:        0
Total transferred:      28800 bytes
HTML transferred:       8100 bytes
Requests per second:    839.62 [#/sec] (mean)
Time per request:       11.910 [ms] (mean)
Time per request:       1.191 [ms] (mean, across all concurrent requests)
Transfer rate:          236.14 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.2      0       1
Processing:     8   11   2.0     10      15
Waiting:        4    8   2.1      7      14
Total:          8   11   2.0     11      16

Percentage of the requests served within a certain time (ms)
  50%     11
  66%     11
  75%     12
  80%     13
  90%     15
  95%     15
  98%     16
  99%     16
 100%     16 (longest request)
```
###### Logger:
```
Server started! localhost :: 8080
{"time":"2020-03-08T19:18:30.501Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.508Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.510Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.515Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.515Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.516Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.516Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.517Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.517Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.518Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.518Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.518Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.519Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.519Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.520Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.520Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.521Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.521Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.522Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:18:30.522Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.522Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.523Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.523Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:18:30.523Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.524Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:18:30.524Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.525Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.525Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.526Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:18:30.526Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.526Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.527Z","lvl":"INFO","msg":"Response with status 200 in 1 ms."}
{"time":"2020-03-08T19:18:30.527Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.530Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.530Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.531Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.531Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.531Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.531Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.532Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.532Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.532Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.533Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.533Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.534Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.534Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.534Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.534Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.535Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.535Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.535Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.535Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.536Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.536Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.536Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.537Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.537Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.537Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.538Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:18:30.538Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.538Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.538Z","lvl":"INFO","msg":"Response with status 200 in 0 ms."}
{"time":"2020-03-08T19:18:30.539Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.541Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.541Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.541Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.542Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.542Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.542Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.543Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.543Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.543Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.544Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.544Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.545Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.545Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.545Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.545Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.546Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.546Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.546Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.546Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.547Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.547Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.547Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.547Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.548Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.548Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.548Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.548Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.549Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.550Z","lvl":"INFO","msg":"Response with status 200 in 1 ms."}
{"time":"2020-03-08T19:18:30.550Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.552Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.552Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.553Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.553Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.553Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.554Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.554Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.554Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.555Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.555Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.555Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.556Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.556Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.559Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:18:30.559Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.560Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.560Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.561Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:18:30.561Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.562Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:18:30.562Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.562Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:18:30.563Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.563Z","lvl":"INFO","msg":"Response with status 200 in 9 ms."}
{"time":"2020-03-08T19:18:30.563Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.564Z","lvl":"INFO","msg":"Response with status 200 in 9 ms."}
{"time":"2020-03-08T19:18:30.564Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.565Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.566Z","lvl":"INFO","msg":"Response with status 200 in 1 ms."}
{"time":"2020-03-08T19:18:30.566Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.568Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.568Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.568Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.569Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.569Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.569Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.569Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.570Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.570Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.571Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.571Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.571Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.571Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.572Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.572Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.572Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.572Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.573Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.573Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.573Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.573Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.574Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.574Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.574Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.574Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.575Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.575Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.575Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.576Z","lvl":"INFO","msg":"Response with status 200 in 1 ms."}
{"time":"2020-03-08T19:18:30.576Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.578Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.578Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.579Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.579Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.579Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.579Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.580Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.580Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.580Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.581Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.581Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.581Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.581Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.582Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.582Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.582Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.582Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.583Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.583Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.583Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.583Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.584Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.584Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.584Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.584Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.585Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.585Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.585Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.587Z","lvl":"INFO","msg":"Response with status 200 in 2 ms."}
{"time":"2020-03-08T19:18:30.587Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.588Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.589Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.589Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.589Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.590Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.590Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.590Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.590Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.591Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.591Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.592Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.592Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.592Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.592Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.593Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.593Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.593Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.593Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.593Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.594Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.594Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.594Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.594Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.595Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.595Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.595Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.596Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.596Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.597Z","lvl":"INFO","msg":"Response with status 200 in 1 ms."}
{"time":"2020-03-08T19:18:30.597Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.599Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.599Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.599Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.599Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.600Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.600Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.600Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.600Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.601Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.601Z","lvl":"INFO","msg":"Response with status 200 in 2 ms."}
{"time":"2020-03-08T19:18:30.601Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.602Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.602Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.602Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.602Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.603Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.603Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.603Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.604Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.604Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.604Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.604Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.605Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.605Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.605Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.605Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.606Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.606Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.607Z","lvl":"INFO","msg":"Response with status 200 in 1 ms."}
{"time":"2020-03-08T19:18:30.607Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.609Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.609Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.609Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.610Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.610Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.610Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.610Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.611Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.611Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.611Z","lvl":"INFO","msg":"Response with status 200 in 2 ms."}
{"time":"2020-03-08T19:18:30.612Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.612Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.612Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.613Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.613Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.613Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.614Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.614Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.614Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.615Z","lvl":"INFO","msg":"Response with status 200 in 5 ms."}
{"time":"2020-03-08T19:18:30.615Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.616Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:18:30.616Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.617Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:18:30.617Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.618Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.619Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.619Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.621Z","lvl":"INFO","msg":"Response with status 200 in 2 ms."}
{"time":"2020-03-08T19:18:30.621Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.623Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.624Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.624Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.625Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.625Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.625Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.626Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.626Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.626Z","lvl":"INFO","msg":"Request from ::1: GET /data"}
{"time":"2020-03-08T19:18:30.627Z","lvl":"INFO","msg":"Response with status 200 in 4 ms."}
{"time":"2020-03-08T19:18:30.627Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.627Z","lvl":"INFO","msg":"Response with status 200 in 3 ms."}
{"time":"2020-03-08T19:18:30.630Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.631Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.631Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.631Z","lvl":"INFO","msg":"Response with status 200 in 6 ms."}
{"time":"2020-03-08T19:18:30.631Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.632Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.632Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.632Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.632Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.633Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.633Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.633Z","lvl":"INFO","msg":"Response with status 200 in 7 ms."}
{"time":"2020-03-08T19:18:30.633Z","lvl":"INFO","msg":"GET request"}
{"time":"2020-03-08T19:18:30.634Z","lvl":"INFO","msg":"Response with status 200 in 8 ms."}
{"time":"2020-03-08T19:18:30.634Z","lvl":"INFO","msg":"GET request"}
```



#### 2. Сконфигурируйте nginx сервер таким образом, чтобы запросы проходили через nginx и перенаправлялись на сервер из лабораторной работы №1.
##### nginx.conf
```
server {
        listen       80;
        server_name  localhost;
        
        location / {
            proxy_pass "http://localhost:8080/";
        }

    }
```

##### GET 
```
$ curl -I http://localhost
HTTP/1.1 200 OK
Server: nginx/1.16.1
Date: Sun, 08 Mar 2020 22:32:18 GMT
Content-Type: text/html; charset=UTF-8
Content-Length: 625
Connection: keep-alive
X-Powered-By: Express
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Sat, 30 Nov 2019 19:03:49 GMT
ETag: W/"271-16ebdb29a08"

$ curl -I http://localhost:8080
HTTP/1.1 200 OK
X-Powered-By: Express
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Sat, 30 Nov 2019 19:03:49 GMT
ETag: W/"271-16ebdb29a08"
Content-Type: text/html; charset=UTF-8
Content-Length: 625
Date: Sun, 08 Mar 2020 22:32:24 GMT
Connection: keep-alive
```

##### 

#### 3. Используйте nginx отдачи статического контента. Как изменилось время ответа сервера?

##### nginx отдает статический контент.
```
server {
        listen       80;
        server_name  localhost;

        
        location / {
            proxy_pass "http://localhost:8080/";
        }

       location /img {
            root /home/user/Desktop/LAB_1/static/;
    }

    }
```
##### Время:

```
Server Software:        nginx/1.16.1
Server Hostname:        localhost
Server Port:            80

Document Path:          /
Document Length:        625 bytes

Concurrency Level:      10
Time taken for tests:   0.192 seconds
Complete requests:      100
Failed requests:        0
Total transferred:      93500 bytes
HTML transferred:       62500 bytes
Requests per second:    520.38 [#/sec] (mean)
Time per request:       19.217 [ms] (mean)
Time per request:       1.922 [ms] (mean, across all concurrent requests)
Transfer rate:          475.15 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       1
Processing:    11   15   3.9     14      39
Waiting:       11   15   3.9     14      38
Total:         11   15   4.0     14      39

Percentage of the requests served within a certain time (ms)
  50%     14
  66%     16
  75%     17
  80%     19
  90%     20
  95%     22
  98%     25
  99%     39
 100%     39 (longest request)

```
#### 4 Настройте кеширование и gzip сжатие файлов.  Как изменилось время ответа сервера?
##### Настройка кеширования и gzip сжатия:
```
http {
    proxy_cache_path /data/cache/nginx levels=1:2 keys_zone=all:32m max_size=1g;
    server {
        listen       80;
        server_name  localhost;

        
        location / {
            proxy_pass "http://localhost:8081/";
            proxy_cache all;
		    proxy_cache_valid any 1h;
		    proxy_cache_valid 404 502 503 1m;
        }
    }

    server {
        listen       8081;
        gzip on;
	    gzip_comp_level 5;

        location / {
            root /home/user/Desktop/LAB_1/static/;
        }
    }
}
```

##### Время:
```
Server Software:        nginx/1.16.1
Server Hostname:        localhost
Server Port:            80

Document Path:          /
Document Length:        625 bytes

Concurrency Level:      10
Time taken for tests:   0.143 seconds
Complete requests:      100
Failed requests:        0
Total transferred:      93500 bytes
HTML transferred:       62500 bytes
Requests per second:    697.49 [#/sec] (mean)
Time per request:       14.337 [ms] (mean)
Time per request:       1.434 [ms] (mean, across all concurrent requests)
Transfer rate:          636.86 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.2      0       1
Processing:     4   14   2.3     14      17
Waiting:        3   14   2.3     14      17
Total:          4   14   2.2     14      17

Percentage of the requests served within a certain time (ms)
  50%     14
  66%     15
  75%     15
  80%     15
  90%     16
  95%     17
  98%     17
  99%     17
 100%     17 (longest request)
```


#### 5 Запустите еще 2 инстанса вашего сервера из лабораторной работы №1, настройте перенаправление таким образом, чтобы на серверы приходили запросы в соотношении 3:1. 

##### 
```
http {
    upstream backend {
        server localhost:8082;
        server localhost:8083;
        server localhost:8084 weight=3;
    }
    server {
        location / {
            proxy_pass http://backend;
        }            
    }
}
```
#### 6. 
```
http {
    map $http_accept_language $browser_lang {
        default ru;
}
    server {
        listen 8080;
        server_name localhost;

        location / {
            proxy_pass http://localhost:8081;
        }
        location /root {
            proxy_pass http://localhost:8082;
        }
    }

    server {
        listen 8081;
        server_name localhost;
        location / {
            root /usr/share/nginx/data/;
            index index1.html style.css;
        }
        location /temp {
            root /usr/share/nginx/data/;
            index index3.html;
        }
        
    }

    server {
        listen 8082;
        server_name localhost;
        location / {
            root /usr/share/nginx/data/;
            index index2.html;
        }
        location /temp {
            root /usr/share/nginx/data/;
            index index4.html;
        }       
    }
}
```

#### 7 Настройте отдачу страницы о состоянии сервера

```
http {
    map $http_accept_language $browser_lang {
        default ru;
}
    server {
        listen 8080;
        server_name localhost;
        
        location = /basic_status {
            stub_status;
        }
        location / {
            proxy_pass http://localhost:8081;
        }
        location /root {
            proxy_pass http://localhost:8082;
        }
    }

    server {
        listen 8081;
        server_name localhost;
        location / {
            root /usr/share/nginx/data/;
            index index1.html style.css;
        }
        location /temp {
            root /usr/share/nginx/data/;
            index index3.html;
        }
        
    }

    server {
        listen 8082;
        server_name localhost;
        location / {
            root /usr/share/nginx/data/;
            index index2.html;
        }
        location /temp {
            root /usr/share/nginx/data/;
            index index4.html;
        }       
    }
}
```