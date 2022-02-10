# Cpp-Techniques
C++ Techniques I Usually Use
よく使うC++テクニック

## Overview
このリポジトリは私がC++プログラムを作成するときによく使うテクニックをまとめたものです。
ここに書かれていることはあくまで個人の原則であり、組織のルールがあればそちらを優先します。

## 命名規則
### 変数、関数
```cpp
std::size_t num_of_tasks = 10;  // スネークケース

int do_something(const int x)  // スネークケース
{   
    int y = 0;
    // do something
    return y;
}
```
### クラス
```cpp
class TerrestrialAnimal  // パスカルケース
{
    private:
    double x_;
    double y_;
    double theta_;
    
    public:
    TerrestrialAnimal(const double x, const double y, const double theta)
    {
        x_ = x;
        y_ = y;
        theta_ = theta;
    }
    
    virtual ~TerrestrialAnimal()
    {

    }
    
    bool set_pose(const double x, const double y, const double theta)  // スネークケース
    {
        // do something
        return true;
    }
};
```
### 配列
原則としてCスタイルの配列は使わない。代わりにstd::arrayやstd::vectorを使う。
```cpp
#include <array>
std::array< uint32_t, 128 > xs;  // 複数形にする
for( auto x:xs )
{
    // do something
}
```
### ポインタ
原則としてCスタイルのポインタは使わない。代わりにスマートポインタを用いる。std::shared_ptrはむやみに使わない。
```cpp
#include <memory>
std::unique_ptr<uint8_t[]> hoge_ptr(new uint8_t[3]);  // 名前は原則"~ptr"
```

## callback関数(関数ポインタ)よりもメンバ関数のoverrideを優先する。
std::functionが使えるならばstd::functionを使うこととする。

```cpp
class Task
{
    public:
    virtual ~Task()
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
