# 32bit,64bit

1. CPU차이
    - 저장장치의 bit폭
    - 레지스터의 크기가 32bit면 32bitCPU/ 64bit면 64bitCPU이다.
    
    <aside>
    💡 레지스터? 연산을 위한 컴퓨터 기억장치
    
    </aside>
    
    - 32bit가 한번에 처리할수 있는 정보는 2^32, 64bit가 한번에 처리할 수 있는 정보는 2^64
    - 레지스터가 크면 한번에 처리할수 있는 정보의 양이 늘어난나
    
    ⇒ bit수가 증가함에 따라 많은 양의 데이터를 처리할 수 있게 되고 기능이 고도화된다.
    
2. 메모리 제한
    - 32bit는 메모리 4GB제한(2^32 = 4,294,967,296)
        
        → why? 레지스터가 한번에 처리할수 있는 용량이 32bit이기 때문이다. cpu가 한번의 인식하여 처리할 수 있는 주소 값의 한계점이 42억개 정도되고 50억 이상의 수를 표현하려면 레지스터의 크가가 32비트로는 부족하다. 간단하게 말해서 32bit의 컴퓨터는 2^32이상 모른다.
        
    - 64bit는 메모리 16EB(엑사바이트)
