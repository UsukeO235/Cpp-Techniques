# Cpp-Techniques
C++ Techniques I Usually Use
よく使うC++テクニック

## Overview
このリポジトリは私がC++プログラムを作成するときによく使うテクニックをまとめたものです。
ここに書かれていることはあくまで個人の原則であり、組織のルールがあればそちらを優先します。

## callback関数(関数ポインタ)よりもメンバ関数のoverrideを優先する。
std::functionが使えるならばstd::functionを使うこととする。

```cpp
class Task
{
    public:
    virtual ~Task(void)
    {
    
    }
    
    virtual void call(void) = 0;  // 純粋仮想関数
};

class UserTask : public Task
{
    private:
    
    public:
    virtual void call(void) override
    {

    }
};

int main()
{
    UserTask ut;
    
    Task* ut_ptr = static_cast<Task*>(&ut);
    
    ut_ptr->call();
    
    return 0;
}
```
