### CPU Burst

CPU 명렁 작업이 연속되는 것

### I/O Burst

로컬 혹은 네트워크의 I/O wait 작업이 연속되는 것

### Bound 의 의미

프로세스를 수행하면서 CPU burst, I/O burst가 번갈아 가며 수행되는데, 수행시간을 더 많이 차지하는 쪽이 bound 한다고 표현한다.

ex) CPU burst가 더 긴 수행 시간을 가지면 CPU Bound,

I/O Burst 가 더 긴 수행 시간을 가지면 I/O Bound