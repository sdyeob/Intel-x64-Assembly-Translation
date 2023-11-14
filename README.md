# Intel-x64-Assembly-Translation

### 1차 번역

## 소개(도입)
 몇년동안, 프로그래머들은 중요한 퍼포먼스를 내는 코드(performance-critical code)를 작성하기 위하여 32bit 어셈블리를 사용했었다. 그러나 32bit(x86) 컴퓨터는 64bit(x64)로 교체되었고, 근본적인 어셈블리 코드는 변화했다.

 이 Gem(..? 해당 아티클을 의미하는 것 같음.)은 64bit 어셈블리를 소개한다. 비록 32bit 어셈블리가 64bit 어셈블리를 이행함에 있어서 쉽게 만들어 줄 지라도, 32bit에 대한 선행 지식은 필요 없다.

 x64는 Intel과 AMD의 32bit x86 지시 세트 아키텍쳐에 확장판에 대한 일반적인 이름이다.
 AMD가 x64의 첫 버전을 도입했다. 이는 초기에는 x86-64로 불렸고, 나중에는 AMD64로 이름이 바뀌었다. 
 Intel은 x64의 초기 이름을 IA-32e로 이름 지었고, 나중에는 EMT64로 변경했다.
 두 버전 사이에는 호환되지 않는 것들(incompatibilities)이 몇개 있지만, 대부분의 작업은 두 버전 모두에서 대체로 가능하다. 세부사항은 Inter64 and IA-32 Architectures Software Developer's Manuals and AMD64 Architecture Tech Docs에서 확인할 수 있다.
 우리는 이것을 교차점에 위치한 x64(과도기의 x64를 나타내는 것 같음)라고 부르고, IA-64라고 불리는 Intel Itanium Architecture과 헷갈려서는 안된다. (We call this intersection flavor x64. Neither is to be confused with the 64bit intel architecture, which is called IA-64)

 해당 Gem에서는 캐쉬, 분기 예측 혹은 다른 고급 개념과 같은 하드웨어적인 세부 사항들은 다루지 않을 것 이다. 해당 분야에 대한 추가적인 정보를 위해서 해당 아티클의 끝에 몇개의 레퍼런스를 달아 두었다.

 비록 대부분의 프로그래머를 위한 좋은 c++ 컴파일러를 능가하는 것은 어렵겠지만, 어셈블리의 경우 프로그램에서 퍼포먼스가 중요한 부분을 위해서 자주 사용된다. 때때로 컴파일러는 부정확한 어셈블리 코드를 생성하고, 디버거에서 코드를 살펴보는 것은 원인을 찾는데 도움이 된다. (sometimes a compiler makes incorrect assembly code and stepping through the code in a debugger helps locate the cause.) 때때로 코드 최적화를 진행하는 데에 있어 실수가 발생하기도 한다. 어셈블리는 때때로 소스코드가 없는 상태에서 해당 코드를 마주하거나 고치는데에 사용될 수 있다. 디스어셈블리는 너가 현존하는 실행 파일을 고치거나 변경하는 것을 가능하게 해준다. 만약 너가 선택한 언어의 밑단에서 어떻게 동작하는지를 알고 싶다면, 어셈블리는 필수적이다. -가령 왜 어떤 것은 빠르고 어떤 것은 느린지에 대한 것 이다. 에섬블리 코드 지식은 기능 고장을 진단해 내는데 있어 필수적(indispensable)이다.


### Architecture
 주어진 플랫폼에 대해서 어셈블리를 학습할 때, 가장 처음 배워야 하는 부분은 레지스터 세트다.

 일반적인 아키텍쳐
 