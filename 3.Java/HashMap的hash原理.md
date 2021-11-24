
### 源码
```Java

static final int hash(Object key) { 
	//jdk1.8 & jdk1.7 
	int h; 
	// h = key.hashCode() 为第一步 取hashCode值 
	// h ^ (h >>> 16) 为第二步 高位参与运算 
	return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16); 
} 

static int indexFor(int h, int length) { 
	//jdk1.7的源码，jdk1.8没有这个方法，但是实现原理一样的 
	return h & (length-1); 
	//第三步 取模运算 
}

```




```Java

// 获取hashCode "abc".hashCode(); 
public int hashCode() { 
	int h = hash; 
	if (h == 0 && value.length > 0) { 
		char val[] = value; 
		for (int i = 0; i < value.length; i++) { 
			h = 31 * h + val[i]; 
		} 
		hash = h; 
	} 
	return h; 
}

```

### 解释
> The value 31 was chosen because it is an odd prime. If it were even and the multiplication overflowed, information would be lost, as multiplication by 2 is equivalent to shifting. The advantage of using a prime is less clear, but it is traditional. A nice property of 31 is that the multiplication can be replaced by a shift and a subtraction for better performance: 31 * i == (i << 5) - i. Modern VMs do this sort of optimization automatically. -- Effective Java

> As Goodrich and Tamassia point out, If you take over 50,000 English words (formed as the union of the word lists provided in two variants of Unix), using the constants 31, 33, 37, 39, and 41 will produce less than 7 collisions in each case. Knowing this, it should come as no surprise that many Java implementations choose one of these constants. --[StackOverFlow](https://stackoverflow.com/questions/299304/why-does-javas-hashcode-in-string-use-31-as-a-multiplier)

### 总结
1. 选用质数可以避免偶数把1位都消除
2. 选用31可以优化成更快速的位移减法操作
3. 经过实验验证碰撞次数比较少