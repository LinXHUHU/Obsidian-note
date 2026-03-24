

```
  

int32_t get_uint8_v_stub(rb::vrte::CalibrationServer* obj, const string& key, std::vector<uint8_t>& v) {

    if(flag_get_uint8_v == 1)

        return 1;

    else if(flag_get_uint8_v == 2)

    {

        std::cout << "[Stub] vector<uint8_t>& v 地址: " << &v << std::endl;

        std::vector<uint8_t> data{1, 2, 0, 0, 0, 0, 0, 0, 0, 2, 1, 2, 1};

        v.assign(data.begin(), data.end());

        for(int a: v)

        {

            std::cout << a << ",";

        }

        std::cout << std::endl;

        std::cout << v.size() << "XXXXXXXXXXXXXXXXXXXXXX" << std::endl;

        return 0;

    }

    else if(flag_get_uint8_v == 3) {

        // std::vector<uint8_t> data{0, 0, 0, 0, 0, 0, 0, 0, 0};

        v.assign({0, 0, 0, 0, 0, 0, 0, 0, 0});

        return 0;

    }

    else

        return -1;

}
```


stub 函数需要加一个参数 表示this 指针 
rb::vrte::CalibrationServer* obj

否则会发生参数偏移导致引用参数 地址不同

![[XC-CP工作文档/asset/Pasted image 20250618143006.png]]

![[XC-CP工作文档/asset/Pasted image 20250618143026.png]]

