# codepratice-day1
代码打卡思考笔记1

代码随想录day1
数组基础、二分法、双指针

数组在c++中内存地址是连续的

二分查找，之前经常记错l,r的赋值问题。代码随想录中提到左闭右开和左闭右闭的区间是否包含概念，可以根据它进行l和r的赋值。

二分的对应题目：[二分查找](https://leetcode.cn/problems/binary-search/)
几种解法（包括之前在acwing学的）:
1.左闭右开区间
```CPP
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int n=nums.size();
        int l=0,r=n;
        while(l<r)//左闭右开区间,起始点不包含n点，因此r应该初始为n.
        {
            int mid=l+r>>1;
            if(nums[mid]<target) l=mid+1;
            else if(nums[mid]>target) r=mid;
            else return mid; 
        }
        return -1;
    }
};
```
2.左闭右闭区间
```CPP
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l=0,r=nums.size()-1;
        while(l<=r)
        {
            int mid=l+r>>1;
            if(nums[mid]>target) r=mid-1;
            else if(nums[mid]<target) l=mid+1;
            else return mid;
        }
        return -1;
    }
};
```
3.acwing的两种解法，第一个是求找到的最前目标，第二个是求找到的最后目标。
```CPP
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l=0,r=nums.size()-1;
        while(l<r)
        {
            int mid=l+r>>1;
            if(nums[mid]>=target) r=mid;
            else l=mid+1;
        }
        if(nums[l]==target) return l;
        else return -1;
    }
};
```
```CPP
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l=0,r=nums.size()-1;
        while(l<r)
        {
            int mid=l+r+1>>1;
            if(nums[mid]<=target) l=mid;
            else r=mid-1;
        }
        if(nums[l]==target) return l;
        else return -1;
    }
};
```

其它的推荐二分题目由于今天时间不够就没写，之后有空补上。

双指针方面，题目为：[移除元素](https://leetcode.cn/problems/remove-element/description/)[有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)
暴力法就是两遍遍历，发现不一样的数，就遍历它之后的数，将这个数和之后的数的位置向前放一位。
移除元素:
```CPP
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slowindex=0;
        for(int fastindex=0;fastindex<nums.size();fastindex++)
        {
            if(nums[fastindex]!=val)
            {
                nums[slowindex++]=nums[fastindex];
            }
        }
        return slowindex;
    }
};
```

有序数组的平方：
```CPP
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int n=nums.size()-1;
        vector<int> ans(n+1,0);
        for(int i=0,j=n;i<=j; )
        {
            if(nums[i]*nums[i]<nums[j]*nums[j])
            {
                ans[n--]=nums[j]*nums[j];
                j--;
            }
            else
            {
                ans[n--]=nums[i]*nums[i];
                i++;
            }
        }
        return ans;
    }
};


```

重点还是理解双指针法。

