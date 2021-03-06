# Java实现单向链表(基础功能实现）

# 详细设计说明
  &nbsp;  &nbsp;  &nbsp;  &nbsp;实现功能的链表以及相关功能由两个类组成:

 - 泛型类Link，命名为Link < T >。该类是链表功能的主类，用于提供链表操作的所有功能。
 - 泛型类Node，命名为Node< T >。表示链表中的节点，该类包含数据元素信息以及指针域信息。由于该节点为Link所独，可以设计成Link的内部类。
 
  &nbsp;  &nbsp;  &nbsp;  &nbsp;每当链表中增加一个元素时，对应增加一个Node对象，Node对象包含了元素信息（泛型变量）以及另一个节点引用对象（即链表指针域，实现多个节点的链接功能）。
## 1 Node类的详细设计说明
  &nbsp;  &nbsp;  &nbsp;  &nbsp;Node类是为链表的节点信息，与主类Link的泛型信息应保持一致。由于该类主要用于链表节点对象声明，建议创建成为Link的内部类。其声明名称应为"static class Node<T>"。为了方便Node的使用，可以为Node增加一个构造方法用于直接初始化节点中的元素信息和指针域信息。Node类的成员变量和一个构造方法声明如下：
	
 - **T item**:变量item用于存储链表节点中的数据（数据区）。 	
 - **Node< T > next**:变量next用于存储下一个链表节点对象（指针域）。 	
   **public Node(T item,Node< T > next)**:构造方法，用于初始化Node的成员变量。

## 2 Link类的详细设计
  &nbsp;  &nbsp;  &nbsp;  &nbsp;Link类是实现功能的主要类，Link的声明应为"public class Link< T >"，链表的基本功能在Link类中进行实现。
### 2.1 Link成员变量

 - **private int size**：用于表示链表的长度，初始值为0。当链表添加和删除节点时，应该修改size的值，size值与链表的实际长度吻合。
 -  **private final int  MAX_SIZE**：用于表示链表的最大长度。该值应为合理的整型常量，链表的长度应小于该值，初始值我们可以根据需求自行定义（不要超过int的最大值）。	
 - **private  Node< T > head**：表示链表的头结点，当删除头结点时，头结点的下一个节点变为头结点，初始值为null。 
 - **private  Node< T > last**：表示链表的尾结点。当删除尾结点时，尾结点的上一个节点变为尾结点，初始值为null。

### 2.2 Link类方法
**1.public boolean add(T e)**

 - **方法描述**：（重载方法）向链表中添加新元素e。返回值为true表明添加成功，失败为false。
 - **实现过程**：1.先判断size>=MAX_SIZE条件是否成立，如果成立说明超出链表长度，方法返回false。2.创建新节点node，其次再判断链表中是否是空链表，如果是空链表，更新头结点和尾节点信息为node。如果不是空链表，在尾节点后添加node节点，并更新尾节点信息。size自增一个单位，方法返回true。
 
 **2.public boolean add(int index,T e)**
 - **方法描述**：（重载方法）在指定的节点index序列前插入新的元素e。返回值为true表明添加成功，失败为false。注意，该方法无法添加在尾节点之后，但可以添加在头节点之前。
 - **实现过程**：1.判断指定索引index是否在链表范围内，并且判断是否会超出链表最大长度，如果不满足条件，方法返回false。2.索引在指定范围内时，创建新节点newNode，先判断目标是否是头节点（即索引为0），如果是头节点，将创建新节点指向头节点，并更新头结点信息。3.如果不是头结点，找到索引处的节点node和索引处前一个节点preNode，再创建新节点信息，并将新节点插入在preNode和node之间，更新节点之间的关系。4.节点添加成功，size自增一个单位，并返回true。

**3.public boolean contains(Object e)**
 - **方法描述**：查询链表中是否有当前对象，对象是否相等取决于equlas方法也是我们判断链表中是否含有目标元素e的重要判断条件。返回值为true表明有该对象，没有找到则为false。
 - **实现过程**：1.遍历链表，判断遍历的元素是否与目标对象e相等，如果被遍历的节点元素与目标节点相等，方法返回true。2.如果遍历完成后，依然没有找到与目标相等的对象，方法返回false。

**4.public T get(int index)**
 - **方法描述**：返回指定序列index处的节点元素信息。如果序列不存在，方法返回null。
 -  **实现过程**：1.当序列索引index不再链表范围内，返回null。2.如果索引在正常范围内，移动到index所在的节点node处，并返回node.item。


**5.public T getHead()**:返回链表的头节点元素，如果头结点为null，返回null。

**6.public T getLast()**:返回链表的尾节点元素，如果尾结点为null，返回null。

**7.public boolean remove(int index)**
 - **方法描述**：删除指定索引index处的节点。返回值为true表明删除成功，失败为false。
 -  **实现过程**：1.当index不再链表序列中，方法返回false。2.索引指向头节点时，头节点后移，并将原头结点删除。3.获取要被删除的节点node和前一节点preNode，如果node是尾节点，更新尾节点为preNode，并删除node节点信息。如果不是尾节点，preNode指向下一个节点，并删除node节点信息。4.删除节点成功，size自减一个单位，并返回true。

**8.public int size()**:返回链表的size变量值。
