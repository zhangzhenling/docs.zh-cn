---
title: "泛型类（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, generic classes
- generics [C#], classes
ms.assetid: 27d6f256-cd61-41e3-bc6e-b990a53b0224
caps.latest.revision: 30
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 17ec9f5d26c01b7f7f7f95026bfdfaa88d709b60
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="generic-classes-c-programming-guide"></a>泛型类（C# 编程指南）
泛型类封装不特定于特定数据类型的操作。 泛型类最常见用法是用于链接列表、哈希表、堆栈、队列和树等集合。 无论存储数据的类型如何，添加项和从集合删除项等操作的执行方式基本相同。  
  
 对于大多数需要集合类的方案，推荐做法是使用 .NET Framework 类库中提供的集合类。 有关使用这些类的详细信息，请参阅 [.NET Framework 类库中的泛型](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md)。  
  
 通常，创建泛型类是从现有具体类开始，然后每次逐个将类型更改为类型参数，直到泛化和可用性达到最佳平衡。 创建自己的泛型类时，需要考虑以下重要注意事项：  
  
-   要将哪些类型泛化为类型参数。  
  
     通常，可参数化的类型越多，代码就越灵活、其可重用性就越高。 但过度泛化会造成其他开发人员难以阅读或理解代码。  
  
-   要将何种约束（如有）应用到类型参数（请参阅[类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)）。  
  
     其中一个有用的规则是，应用最大程度的约束，同时仍可处理必须处理的类型。 例如，如果知道泛型类仅用于引用类型，则请应用类约束。 这可防止将类意外用于值类型，并使你可在 `T` 上使用 `as` 运算符和检查 null 值。  
  
-   是否将泛型行为分解为基类和子类。  
  
     因为泛型类可用作基类，所以非泛型类的相同设计注意事项在此也适用。 请参阅本主题后文有关从泛型基类继承的规则。  
  
-   实现一个泛型接口还是多个泛型接口。  
  
     例如，如果要设计用于在基于泛型的集合中创建项的类，则可能必须实现一个接口，例如 <xref:System.IComparable%601>，其中 `T` 为类的类型。  
  
 有关简单泛型类的示例，请参阅[泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)。  
  
 类型参数和约束的规则对于泛型类行为具有多种含义，尤其是在继承性和成员可访问性方面。 应当了解一些术语，然后再继续。 对于泛型类 `Node<T>,`客户端代码可通过指定类型参数来引用类，创建封闭式构造类型 (`Node<int>`)。 或者，可以不指定类型参数（例如指定泛型基类时），创建开放式构造类型 (`Node<T>`)。 泛型类可继承自具体的封闭式构造或开放式构造基类：  
  
 [!code-cs[csProgGuideGenerics#16](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_1.cs)]  
  
 非泛型类（即，具体类）可继承自封闭式构造基类，但不可继承自开放式构造类或类型参数，因为运行时客户端代码无法提供实例化基类所需的类型参数。  
  
 [!code-cs[csProgGuideGenerics#17](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_2.cs)]  
  
 继承自开放式构造类型的泛型类必须对非此继承类共享的任何基类类型参数提供类型参数，如下方代码所示：  
  
 [!code-cs[csProgGuideGenerics#18](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_3.cs)]  
  
 继承自开放式构造类型的泛型类必须指定作为基类型上约束超集或表示这些约束的约束：  
  
 [!code-cs[csProgGuideGenerics#19](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_4.cs)]  
  
 泛型类型可使用多个类型参数和约束，如下所示：  
  
 [!code-cs[csProgGuideGenerics#20](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_5.cs)]  
  
 开放式构造和封闭式构造类型可用作方法参数：  
  
 [!code-cs[csProgGuideGenerics#21](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_6.cs)]  
  
 如果一个泛型类实现一个接口，则该类的所有实例均可强制转换为该接口。  
  
 泛型类是不变量。 换而言之，如果一个输入参数指定 `List<BaseClass>`，且你尝试提供 `List<DerivedClass>`，则会出现编译时错误。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Generic>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [泛型](../../../csharp/programming-guide/generics/index.md)   
 [Saving the State of Enumerators](http://go.microsoft.com/fwlink/?LinkId=112390) （保存枚举器状态）  
 [An Inheritance Puzzle, Part One](http://go.microsoft.com/fwlink/?LinkId=112380)（继承测验，第一部分）

