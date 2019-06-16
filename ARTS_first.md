

##### Algorithm

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]



方法一：自己的解法就是网上给出的暴力法，其他方法就没有想到，还得多练习。
暴力法很简单，遍历每个元素 xx，并查找是否存在一个值与 target - xtarget−x 相等的目标元素。

    public int[] twoSum(int[] nums, int target) {
      for (int i = 0; i < nums.length; i++) {
          for (int j = i + 1; j < nums.length; j++) {
              if (nums[j] == target - nums[i]) {
                  return new int[] { i, j };
              }
          }
      }
      throw new IllegalArgumentException("No two sum solution");
    }
复杂度分析：

时间复杂度：O(n^2)O(n 2 )， 对于每个元素，我们试图通过遍历数组的其余部分来寻找它所对应的目标元素，这将耗费 O(n)O(n) 的时间。因此时间复杂度为 O(n^2)O(n 2 )。

空间复杂度：O(1)O(1)。

方法二：两遍哈希表
为了对运行时间复杂度进行优化，我们需要一种更有效的方法来检查数组中是否存在目标元素。如果存在，我们需要找出它的索引。保持数组中的每个元素与其索引相互对应的最好方法是什么？哈希表。

通过以空间换取速度的方式，我们可以将查找时间从 O(n)O(n) 降低到 O(1)O(1)。哈希表正是为此目的而构建的，它支持以 近似 恒定的时间进行快速查找。我用“近似”来描述，是因为一旦出现冲突，查找用时可能会退化到 O(n)O(n)。但只要你仔细地挑选哈希函数，在哈希表中进行查找的用时应当被摊销为 O(1)O(1)。

一个简单的实现使用了两次迭代。在第一次迭代中，我们将每个元素的值和它的索引添加到表中。然后，在第二次迭代中，我们将检查每个元素所对应的目标元素（target - nums[i]target−nums[i]）是否存在于表中。注意，该目标元素不能是 nums[i]nums[i] 本身！


    public int[] twoSum(int[] nums, int target) {
      Map<Integer, Integer> map = new HashMap<>();
      for (int i = 0; i < nums.length; i++) {
          map.put(nums[i], i);
      }
      for (int i = 0; i < nums.length; i++) {
          int complement = target - nums[i];
          if (map.containsKey(complement) && map.get(complement) != i) {
              return new int[] { i, map.get(complement) };
          }
      }
      throw new IllegalArgumentException("No two sum solution");
    }
复杂度分析：

时间复杂度：O(n)O(n)， 我们把包含有 nn 个元素的列表遍历两次。由于哈希表将查找时间缩短到 O(1)O(1) ，所以时间复杂度为 O(n)O(n)。

空间复杂度：O(n)O(n)， 所需的额外空间取决于哈希表中存储的元素数量，该表中存储了 nn 个元素。

方法三：一遍哈希表
事实证明，我们可以一次完成。在进行迭代并将元素插入到表中的同时，我们还会回过头来检查表中是否已经存在当前元素所对应的目标元素。如果它存在，那我们已经找到了对应解，并立即将其返回。


    public int[] twoSum(int[] nums, int target) {
      Map<Integer, Integer> map = new HashMap<>();
      for (int i = 0; i < nums.length; i++) {
          int complement = target - nums[i];
          if (map.containsKey(complement)) {
              return new int[] { map.get(complement), i };
          }
          map.put(nums[i], i);
      }
      throw new IllegalArgumentException("No two sum solution");
    }

复杂度分析：

时间复杂度：O(n)O(n)， 我们只遍历了包含有 nn 个元素的列表一次。在表中进行的每次查找只花费 O(1)O(1) 的时间。

空间复杂度：O(n)O(n)， 所需的额外空间取决于哈希表中存储的元素数量，该表最多需要存储 nn 个元素。



##### Review

[https://dzone.com/articles/reflection-is-the-most-important-java-api](https://dzone.com/articles/reflection-is-the-most-important-java-api)

就在前几天，我突然想知道：最重要的Java API是什么？哪个SE和EE  API能够使大多数Java生态系统成为可能，并且不能仅仅被重新创建为第三方库？

正如你可能已经猜到的那样 - 我认为它是反射 API。 是的，它不可避免地直接或间接地成为每个项目的一部分。 但对于更多API，尤其是Collection API，情况确实如此。 但是，Reflection API的重要之处在于它支持了当今大多数流行的工具和框架 -  Spring，Hibernate，大量的Web框架。

大多数其他API可以在JDK之外实现。 Collections API在公共收集方面表现得非常好。 它是JDK的一部分更好，但我们可以在没有它的情况下进行管理（它出现在Java 1.2中）。 但反射API不能。 它几乎必须是语言的一个组成部分。

没有反射，你就不能拥有我们今天使用的任何花哨的工具。 没有ORM，没有依赖注入框架，也没有大多数Web框架。 嗯，从技术上讲，你可以在某些时候有一个主题 - 使用SPI，或仅使用java-config。有人可能会争辩说，如果不是为了反射，我们已经跳过了整个XML配置时代，我们直接需要基于代码的配置。 但它不仅仅依赖于所有这些框架中的反射。即使Spring在配置期间实例化bean并通过将它们转换为InitalizingBean进行初始化，如何在没有反射的情况下处理自动连线注入（“手动”不计算，因为它不是自动连线）？在Hibernate中，内省和Java bean API似乎已经足够了，但是当你深入挖掘时，它们就不够用了。 一般而言，处理注释是不可能的。

如果没有这些框架，Java就不会成为当今这样普及的技术。 如果我们没有庞大的开源生态系统，那么Java将更像是一个利基市场。 当然，这不是唯一的因素 - 语言设计者和JVM实现者有多种东西是正确的。 我想，反射是其中之一。

是的，使用反射感觉很糟糕。 在非框架代码中的反射感觉就像最后一种采取的东西 - 如果给定的库没有为扩展设计得当，在使用它的时候你需要调整它以适应你的情况。 但即使您的代码库中没有反射代码，您的项目也可能充满它，如果没有它，就不可能实现。

使用反射的需要可能被视为语言的缺陷之一 - 你不能用语言给你的东西做重要的东西，所以你求助于一个神奇的API，让你无限制地访问精心设计的API。 我必须得说，即使有反射也是一种事实上的语言特征。 而且它可能在使Java如此受欢迎和普及方面发挥了关键作用。



##### Tips

EXIST查询和IN查询在某些情况下课可以得到相同的结果，具体执行起来哪个效率高呢？

如：

SELECT * FROM A WHERE cc IN (SELECT cc FROM B)

SELECT * FROM A WHERE EXIST (SELECT cc FROM B WHERE B.cc = A.cc)

上面两条SQL语句，如果表A比表B大，那么IN子查询效率比EXIST子查询效率高。



##### Share

分享一个自己最近在看的公众号吧《半佛仙人》。微信公众号搜索这四个字就可以找到，博主分享了自己对于社会上一些黑产的看法，非常有深度和尺度，所以很多文章一段时间就会被删，希望大家也去看看。