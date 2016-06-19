##1、JavaScript值类型和引用类型有哪些
    （1）值类型：数值、布尔值、null、undefined。
    （2）引用类型：对象、数组、函数。

##2、如何理解值类型和引用类型及举例

    我们可以用“连锁店”和“连锁店钥匙”来理解，不知道以下比喻合不合适，^-^。

    （1）值类型理解：变量的交换等于在一个新的地方按照连锁店的规范标准（统一店面理解为相同的变量内容）新开一个分店，这样新开的店与其它旧店互不相关、各自运营。

    【值类型例子】

    复制代码
    function chainStore()
    {
        var store1='Nike China';
        var store2=store1;
        store1='Nike U.S.A.';
        alert(store2); //Nike China
    }
    chainStore();
    //把一个值类型（也可以叫基本类型）store2传递给另一个变量（赋值）时，其实是分配了一块新的内存空间，因此改变store1的值对store2没有任何影响，因为它不像引用类型，变量的交换其实是交换了指像同一个内容的地址。
    复制代码
    （2）引用类型理解：变量的交换等于把现有一间店的钥匙（变量引用地址）复制一把给了另外一个老板，此时两个老板同时管理一间店，两个老板的行为都有可能对一间店的运营造成影响。

    【引用类型例子】

    复制代码
    function chainStore()
    {
        var store1=['Nike China'];
        var store2=store1;
        alert(store2[0]); //Nike China
        store1[0]='Nike U.S.A.';
        alert(store2[0]); //Nike U.S.A.
    }
    chainStore();
    //在上面的代码中，store2只进行了一次赋值，理论上它的值已定，但后面通过改写store1的值，发现store2的值也发生了改变，这正是引用类型的特征，也是我们要注意的地方。
    复制代码