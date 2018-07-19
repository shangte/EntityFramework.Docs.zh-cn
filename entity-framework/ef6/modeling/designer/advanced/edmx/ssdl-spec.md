---
title: SSDL 规范的 EF6
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: a4af4b1a-40f4-48cc-b2e0-fa8f5d9d5419
caps.latest.revision: 3
ms.openlocfilehash: a9977c80d9a9401afdcad2284a705bcb28790fb8
ms.sourcegitcommit: 9ae4473425c5e76337c9d032b0e5dbfedf1fcf57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2018
ms.locfileid: "39120540"
---
# <a name="ssdl-specification"></a><span data-ttu-id="508bb-102">SSDL 规范</span><span class="sxs-lookup"><span data-stu-id="508bb-102">SSDL Specification</span></span>
<span data-ttu-id="508bb-103">存储架构定义语言 (SSDL) 是一种基于 XML 的语言，用于描述实体框架应用程序的存储模型。</span><span class="sxs-lookup"><span data-stu-id="508bb-103">Store schema definition language (SSDL) is an XML-based language that describes the storage model of an Entity Framework application.</span></span>

<span data-ttu-id="508bb-104">在实体框架应用程序，存储模型元数据是加载从.ssdl 文件 （用 SSDL 编写） 到 System.Data.Metadata.Edm.StoreItemCollection 的实例，是可访问通过使用中的方法System.Data.Metadata.Edm.MetadataWorkspace 类。</span><span class="sxs-lookup"><span data-stu-id="508bb-104">In an Entity Framework application, storage model metadata is loaded from a .ssdl file (written in SSDL) into an instance of the System.Data.Metadata.Edm.StoreItemCollection and is accessible by using methods in the System.Data.Metadata.Edm.MetadataWorkspace class.</span></span> <span data-ttu-id="508bb-105">实体框架使用存储模型元数据将针对特定于应用商店的命令对概念模型的查询。</span><span class="sxs-lookup"><span data-stu-id="508bb-105">Entity Framework uses storage model metadata to translate queries against the conceptual model to store-specific commands.</span></span>

<span data-ttu-id="508bb-106">实体框架设计器 （EF 设计器） 在.edmx 文件中存储模型信息存储在设计时。</span><span class="sxs-lookup"><span data-stu-id="508bb-106">The Entity Framework Designer (EF Designer) stores storage model information in an .edmx file at design time.</span></span> <span data-ttu-id="508bb-107">在生成时实体设计器使用.edmx 文件中的信息创建在运行时所需的实体框架的.ssdl 文件。</span><span class="sxs-lookup"><span data-stu-id="508bb-107">At build time the Entity Designer uses information in an .edmx file to create the .ssdl file that is needed by Entity Framework at runtime.</span></span>

<span data-ttu-id="508bb-108">SSDL 的版本按 XML 命名空间进行区分。</span><span class="sxs-lookup"><span data-stu-id="508bb-108">Versions of SSDL are differentiated by XML namespaces.</span></span>

| <span data-ttu-id="508bb-109">SSDL 版本</span><span class="sxs-lookup"><span data-stu-id="508bb-109">SSDL Version</span></span> | <span data-ttu-id="508bb-110">XML Namespace</span><span class="sxs-lookup"><span data-stu-id="508bb-110">XML Namespace</span></span>                                     |
|:-------------|:--------------------------------------------------|
| <span data-ttu-id="508bb-111">SSDL v1</span><span class="sxs-lookup"><span data-stu-id="508bb-111">SSDL v1</span></span>      | http://schemas.microsoft.com/ado/2006/04/edm/ssdl |
| <span data-ttu-id="508bb-112">SSDL v2</span><span class="sxs-lookup"><span data-stu-id="508bb-112">SSDL v2</span></span>      | http://schemas.microsoft.com/ado/2009/02/edm/ssdl |
| <span data-ttu-id="508bb-113">SSDL v3</span><span class="sxs-lookup"><span data-stu-id="508bb-113">SSDL v3</span></span>      | http://schemas.microsoft.com/ado/2009/11/edm/ssdl |

## <a name="association-element-ssdl"></a><span data-ttu-id="508bb-114">Association 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-114">Association Element (SSDL)</span></span>

<span data-ttu-id="508bb-115">**关联**存储架构定义语言 (SSDL) 中的元素指定参与的表列中基础数据库中的外键约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-115">An **Association** element in store schema definition language (SSDL) specifies table columns that participate in a foreign key constraint in the underlying database.</span></span> <span data-ttu-id="508bb-116">两个必需的子 End 元素指定位于关联各端的表和每一端的重数。</span><span class="sxs-lookup"><span data-stu-id="508bb-116">Two required child End elements specify tables at the ends of the association and the multiplicity at each end.</span></span> <span data-ttu-id="508bb-117">可选 ReferentialConstraint 元素指定的主体端和依赖端的关联，以及参与列。</span><span class="sxs-lookup"><span data-stu-id="508bb-117">An optional ReferentialConstraint element specifies the principal and dependent ends of the association as well as the participating columns.</span></span> <span data-ttu-id="508bb-118">如果没有**ReferentialConstraint**元素存在，必须使用 AssociationSetMapping 元素来指定列映射的关联。</span><span class="sxs-lookup"><span data-stu-id="508bb-118">If no **ReferentialConstraint** element is present, an AssociationSetMapping element must be used to specify the column mappings for the association.</span></span>

<span data-ttu-id="508bb-119">**关联**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-119">The **Association** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-120">文档 （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-120">Documentation (zero or one)</span></span>
-   <span data-ttu-id="508bb-121">结束 （正好两个）</span><span class="sxs-lookup"><span data-stu-id="508bb-121">End (exactly two)</span></span>
-   <span data-ttu-id="508bb-122">ReferentialConstraint （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-122">ReferentialConstraint (zero or one)</span></span>
-   <span data-ttu-id="508bb-123">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-123">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-124">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-124">Applicable Attributes</span></span>

<span data-ttu-id="508bb-125">下表介绍可应用于的特性**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-125">The following table describes the attributes that can be applied to the **Association** element.</span></span>

| <span data-ttu-id="508bb-126">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-126">Attribute Name</span></span> | <span data-ttu-id="508bb-127">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-127">Is Required</span></span> | <span data-ttu-id="508bb-128">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-128">Value</span></span>                                                                            |
|:---------------|:------------|:---------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-129">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-129">**Name**</span></span>       | <span data-ttu-id="508bb-130">是</span><span class="sxs-lookup"><span data-stu-id="508bb-130">Yes</span></span>         | <span data-ttu-id="508bb-131">基础数据库中相应外键约束的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-131">The name of the corresponding foreign key constraint in the underlying database.</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-132">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-132">Any number of annotation attributes (custom XML attributes) may be applied to the **Association** element.</span></span> <span data-ttu-id="508bb-133">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-133">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-134">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-134">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-135">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-135">Example</span></span>

<span data-ttu-id="508bb-136">下面的示例演示**关联**使用的元素**ReferentialConstraint**元素指定参与的列**FK\_CustomerOrders**外键约束：</span><span class="sxs-lookup"><span data-stu-id="508bb-136">The following example shows an **Association** element that uses a **ReferentialConstraint** element to specify the columns that participate in the **FK\_CustomerOrders** foreign key constraint:</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```

## <a name="associationset-element-ssdl"></a><span data-ttu-id="508bb-137">AssociationSet 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-137">AssociationSet Element (SSDL)</span></span>

<span data-ttu-id="508bb-138">**AssociationSet**存储架构定义语言 (SSDL) 中的元素表示基础数据库中的两个表之间的外键约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-138">The **AssociationSet** element in store schema definition language (SSDL) represents a foreign key constraint between two tables in the underlying database.</span></span> <span data-ttu-id="508bb-139">Association 元素中指定参与外键约束的表格列。</span><span class="sxs-lookup"><span data-stu-id="508bb-139">The table columns that participate in the foreign key constraint are specified in an Association element.</span></span> <span data-ttu-id="508bb-140">**关联**元素对应于给定**AssociationSet**元素中指定**关联**属性的**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-140">The **Association** element that corresponds to a given **AssociationSet** element is specified in the **Association** attribute of the **AssociationSet** element.</span></span>

<span data-ttu-id="508bb-141">SSDL 关联集的 AssociationSetMapping 元素映射到 CSDL 关联集。</span><span class="sxs-lookup"><span data-stu-id="508bb-141">SSDL association sets are mapped to CSDL association sets by an AssociationSetMapping element.</span></span> <span data-ttu-id="508bb-142">但是，如果给定的 CSDL 关联 CSDL 关联集定义使用 ReferentialConstraint 元素，没有相应**AssociationSetMapping**元素是必要的。</span><span class="sxs-lookup"><span data-stu-id="508bb-142">However, if the CSDL association for a given CSDL association set is defined by using a ReferentialConstraint element , no corresponding **AssociationSetMapping** element is necessary.</span></span> <span data-ttu-id="508bb-143">在这种情况下，如果**AssociationSetMapping**元素存在，它定义的映射将被重写由**ReferentialConstraint**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-143">In this case, if an **AssociationSetMapping** element is present, the mappings it defines will be overridden by the **ReferentialConstraint** element.</span></span>

<span data-ttu-id="508bb-144">**AssociationSet**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-144">The **AssociationSet** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-145">文档 （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-145">Documentation (zero or one)</span></span>
-   <span data-ttu-id="508bb-146">结束 （零个或两个）</span><span class="sxs-lookup"><span data-stu-id="508bb-146">End (zero or two)</span></span>
-   <span data-ttu-id="508bb-147">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-147">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-148">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-148">Applicable Attributes</span></span>

<span data-ttu-id="508bb-149">下表介绍可应用于的特性**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-149">The following table describes the attributes that can be applied to the **AssociationSet** element.</span></span>

| <span data-ttu-id="508bb-150">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-150">Attribute Name</span></span>  | <span data-ttu-id="508bb-151">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-151">Is Required</span></span> | <span data-ttu-id="508bb-152">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-152">Value</span></span>                                                                                                |
|:----------------|:------------|:-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-153">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-153">**Name**</span></span>        | <span data-ttu-id="508bb-154">是</span><span class="sxs-lookup"><span data-stu-id="508bb-154">Yes</span></span>         | <span data-ttu-id="508bb-155">关联集表示的外键约束的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-155">The name of the foreign key constraint that the association set represents.</span></span>                          |
| <span data-ttu-id="508bb-156">**关联**</span><span class="sxs-lookup"><span data-stu-id="508bb-156">**Association**</span></span> | <span data-ttu-id="508bb-157">是</span><span class="sxs-lookup"><span data-stu-id="508bb-157">Yes</span></span>         | <span data-ttu-id="508bb-158">定义参与外键约束的列的关联的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-158">The name of the association that defines the columns that participate in the foreign key constraint.</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-159">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-159">Any number of annotation attributes (custom XML attributes) may be applied to the **AssociationSet** element.</span></span> <span data-ttu-id="508bb-160">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-160">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-161">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-161">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-162">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-162">Example</span></span>

<span data-ttu-id="508bb-163">下面的示例演示**AssociationSet**元素，它表示`FK_CustomerOrders`基础数据库中的外键约束：</span><span class="sxs-lookup"><span data-stu-id="508bb-163">The following example shows an **AssociationSet** element that represents the `FK_CustomerOrders` foreign key constraint in the underlying database:</span></span>

``` xml
 <AssociationSet Name="FK_CustomerOrders"
                 Association="ExampleModel.Store.FK_CustomerOrders">
   <End Role="Customers" EntitySet="Customers" />
   <End Role="Orders" EntitySet="Orders" />
 </AssociationSet>
```

## <a name="collectiontype-element-ssdl"></a><span data-ttu-id="508bb-164">CollectionType 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-164">CollectionType Element (SSDL)</span></span>

<span data-ttu-id="508bb-165">**CollectionType**存储架构定义语言 (SSDL) 中的元素指定函数的返回类型是集合。</span><span class="sxs-lookup"><span data-stu-id="508bb-165">The **CollectionType** element in store schema definition language (SSDL) specifies that a function’s return type is a collection.</span></span> <span data-ttu-id="508bb-166">**CollectionType**元素是 ReturnType 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-166">The **CollectionType** element is a child of the ReturnType element.</span></span> <span data-ttu-id="508bb-167">使用 RowType 子元素指定集合的类型：</span><span class="sxs-lookup"><span data-stu-id="508bb-167">The type of collection is specified by using the RowType child element:</span></span>

> [!NOTE]
> <span data-ttu-id="508bb-168">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**CollectionType**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-168">Any number of annotation attributes (custom XML attributes) may be applied to the **CollectionType** element.</span></span> <span data-ttu-id="508bb-169">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-169">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-170">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-170">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-171">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-171">Example</span></span>

<span data-ttu-id="508bb-172">下面的示例演示使用的函数**CollectionType**元素来指定该函数返回的行集合。</span><span class="sxs-lookup"><span data-stu-id="508bb-172">The following example shows a function that uses a **CollectionType** element to specify that the function returns a collection of rows.</span></span>

``` xml
   <Function Name="GetProducts" IsComposable="true" Schema="dbo">
     <ReturnType>
       <CollectionType>
         <RowType>
           <Property Name="ProductID" Type="int" Nullable="false" />
           <Property Name="CategoryID" Type="bigint" Nullable="false" />
           <Property Name="ProductName" Type="nvarchar" MaxLength="40" Nullable="false" />
           <Property Name="UnitPrice" Type="money" />
           <Property Name="Discontinued" Type="bit" />
         </RowType>
       </CollectionType>
     </ReturnType>
   </Function>
```

## <a name="commandtext-element-ssdl"></a><span data-ttu-id="508bb-173">CommandText 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-173">CommandText Element (SSDL)</span></span>

<span data-ttu-id="508bb-174">**CommandText**存储架构定义语言 (SSDL) 中的元素是允许你定义在数据库中执行的 SQL 语句在 Function 元素的子级。</span><span class="sxs-lookup"><span data-stu-id="508bb-174">The **CommandText** element in store schema definition language (SSDL) is a child of the Function element that allows you to define a SQL statement that is executed at the database.</span></span> <span data-ttu-id="508bb-175">**CommandText**元素可用于添加类似于在数据库中，存储过程的功能，但不是定义**CommandText**存储模型中的元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-175">The **CommandText** element allows you to add functionality that is similar to a stored procedure in the database, but you define the **CommandText** element in the storage model.</span></span>

<span data-ttu-id="508bb-176">**CommandText**元素不能具有子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-176">The **CommandText** element cannot have child elements.</span></span> <span data-ttu-id="508bb-177">正文**CommandText**元素必须是有效的 SQL 语句的基础数据库。</span><span class="sxs-lookup"><span data-stu-id="508bb-177">The body of the **CommandText** element must be a valid SQL statement for the underlying database.</span></span>

<span data-ttu-id="508bb-178">任何属性都适用于**CommandText**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-178">No attributes are applicable to the **CommandText** element.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-179">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-179">Example</span></span>

<span data-ttu-id="508bb-180">下面的示例演示**函数**具有一个子元素**CommandText**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-180">The following example shows a **Function** element with a child **CommandText** element.</span></span> <span data-ttu-id="508bb-181">公开**UpdateProductInOrder**通过导入到概念模型函数作为 ObjectContext 的方法。</span><span class="sxs-lookup"><span data-stu-id="508bb-181">Expose the **UpdateProductInOrder** function as a method on the ObjectContext by importing it into the conceptual model.</span></span>  

``` xml
 <Function Name="UpdateProductInOrder" IsComposable="false">
   <CommandText>
     UPDATE Orders
     SET ProductId = @productId
     WHERE OrderId = @orderId;
   </CommandText>
   <Parameter Name="productId"
              Mode="In"
              Type="int"/>
   <Parameter Name="orderId"
              Mode="In"
              Type="int"/>
 </Function>
```

## <a name="definingquery-element-ssdl"></a><span data-ttu-id="508bb-182">DefiningQuery 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-182">DefiningQuery Element (SSDL)</span></span>

<span data-ttu-id="508bb-183">**DefiningQuery**存储架构定义语言 (SSDL) 中的元素，你可以在基础数据库中直接执行 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="508bb-183">The **DefiningQuery** element in store schema definition language (SSDL) allows you to execute a SQL statement directly in the underlying database.</span></span> <span data-ttu-id="508bb-184">**DefiningQuery**元素通常使用数据库视图类似，但该视图定义存储模型而不是数据库中。</span><span class="sxs-lookup"><span data-stu-id="508bb-184">The **DefiningQuery** element is commonly used like a database view, but the view is defined in the storage model instead of the database.</span></span> <span data-ttu-id="508bb-185">中定义的视图**DefiningQuery**元素都可以映射到概念模型通过 EntitySetMapping 元素中的实体类型。</span><span class="sxs-lookup"><span data-stu-id="508bb-185">The view defined in a **DefiningQuery** element can be mapped to an entity type in the conceptual model through an EntitySetMapping element.</span></span> <span data-ttu-id="508bb-186">这些映射是只读的。</span><span class="sxs-lookup"><span data-stu-id="508bb-186">These mappings are read-only.</span></span>  

<span data-ttu-id="508bb-187">下面的 SSDL 语法显示如何声明**EntitySet**跟**DefiningQuery**元素，其中包含用于检索视图的查询。</span><span class="sxs-lookup"><span data-stu-id="508bb-187">The following SSDL syntax shows the declaration of an **EntitySet** followed by the **DefiningQuery** element that contains a query used to retrieve the view.</span></span>

``` xml
 <Schema>
     <EntitySet Name="Tables" EntityType="Self.STable">
         <DefiningQuery>
           SELECT  TABLE_CATALOG,
                   'test' as TABLE_SCHEMA,
                   TABLE_NAME
           FROM    INFORMATION_SCHEMA.TABLES
         </DefiningQuery>
     </EntitySet>
 </Schema>
```

<span data-ttu-id="508bb-188">可以使用实体框架中的存储的过程对视图启用读写方案。</span><span class="sxs-lookup"><span data-stu-id="508bb-188">You can use stored procedures in the Entity Framework to enable read-write scenarios over views.</span></span> <span data-ttu-id="508bb-189">用于检索数据和更改处理由存储过程，可以为基本的表使用数据源视图或 Entity SQL 视图。</span><span class="sxs-lookup"><span data-stu-id="508bb-189">You can use either a data source view or an Entity SQL view as the base table for retrieving data and for change processing by stored procedures.</span></span>

<span data-ttu-id="508bb-190">可以使用**DefiningQuery**元素用于目标 Microsoft SQL Server Compact 3.5。</span><span class="sxs-lookup"><span data-stu-id="508bb-190">You can use the **DefiningQuery** element to target Microsoft SQL Server Compact 3.5.</span></span> <span data-ttu-id="508bb-191">尽管 SQL Server Compact 3.5 不支持存储的过程，您可以实现类似功能与**DefiningQuery**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-191">Though SQL Server Compact 3.5 does not support stored procedures, you can implement similar functionality with the **DefiningQuery** element.</span></span> <span data-ttu-id="508bb-192">另一个有用之处在于，可以创建存储过程以克服编程语言中使用的数据类型与数据源的数据类型的不匹配。</span><span class="sxs-lookup"><span data-stu-id="508bb-192">Another place where it can be useful is in creating stored procedures to overcome a mismatch between the data types used in the programming language and those of the data source.</span></span> <span data-ttu-id="508bb-193">你可以编写**DefiningQuery** ，采用特定的参数集，然后调用带有一组不同的参数，例如，删除数据的存储过程的存储的过程。</span><span class="sxs-lookup"><span data-stu-id="508bb-193">You could write a **DefiningQuery** that takes a certain set of parameters and then calls a stored procedure with a different set of parameters, for example, a stored procedure that deletes data.</span></span>

## <a name="dependent-element-ssdl"></a><span data-ttu-id="508bb-194">Dependent 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-194">Dependent Element (SSDL)</span></span>

<span data-ttu-id="508bb-195">**依赖**存储架构定义语言 (SSDL) 中的元素是定义 （也称为引用约束） 的外键约束的依赖端 ReferentialConstraint 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-195">The **Dependent** element in store schema definition language (SSDL) is a child element to the ReferentialConstraint element that defines the dependent end of a foreign key constraint (also called a referential constraint).</span></span> <span data-ttu-id="508bb-196">**依赖**元素引用的主键列 （或列） 的表中指定的列 （或列）。</span><span class="sxs-lookup"><span data-stu-id="508bb-196">The **Dependent** element specifies the column (or columns) in a table that reference a primary key column (or columns).</span></span> <span data-ttu-id="508bb-197">**PropertyRef**元素指定所引用的列。</span><span class="sxs-lookup"><span data-stu-id="508bb-197">**PropertyRef** elements specify which columns are referenced.</span></span> <span data-ttu-id="508bb-198">主体元素指定的列中指定的引用的主键列**依赖**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-198">The Principal element specifies the primary key columns that are referenced by columns that are specified in the **Dependent** element.</span></span>

<span data-ttu-id="508bb-199">**依赖**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-199">The **Dependent** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-200">PropertyRef （一个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-200">PropertyRef (one or more)</span></span>
-   <span data-ttu-id="508bb-201">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-201">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-202">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-202">Applicable Attributes</span></span>

<span data-ttu-id="508bb-203">下表介绍可应用于的特性**依赖**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-203">The following table describes the attributes that can be applied to the **Dependent** element.</span></span>

| <span data-ttu-id="508bb-204">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-204">Attribute Name</span></span> | <span data-ttu-id="508bb-205">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-205">Is Required</span></span> | <span data-ttu-id="508bb-206">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-206">Value</span></span>                                                                                                                                                       |
|:---------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-207">**角色**</span><span class="sxs-lookup"><span data-stu-id="508bb-207">**Role**</span></span>       | <span data-ttu-id="508bb-208">是</span><span class="sxs-lookup"><span data-stu-id="508bb-208">Yes</span></span>         | <span data-ttu-id="508bb-209">相同的值**角色**相应的结束元素的特性 （若使用）; 否则为的表的名称包含的引用列。</span><span class="sxs-lookup"><span data-stu-id="508bb-209">The same value as the **Role** attribute (if used) of the corresponding End element; otherwise, the name of the table that contains the referencing column.</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-210">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**依赖**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-210">Any number of annotation attributes (custom XML attributes) may be applied to the **Dependent** element.</span></span> <span data-ttu-id="508bb-211">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-211">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="508bb-212">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-212">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-213">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-213">Example</span></span>

<span data-ttu-id="508bb-214">下面的示例演示使用 Association 元素**ReferentialConstraint**元素指定参与的列**FK\_CustomerOrders**外键约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-214">The following example shows an Association element that uses a **ReferentialConstraint** element to specify the columns that participate in the **FK\_CustomerOrders** foreign key constraint.</span></span> <span data-ttu-id="508bb-215">**依赖**元素指定**CustomerId**的列**顺序**表约束的依赖端。</span><span class="sxs-lookup"><span data-stu-id="508bb-215">The **Dependent** element specifies the **CustomerId** column of the **Order** table as the dependent end of the constraint.</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```

## <a name="documentation-element-ssdl"></a><span data-ttu-id="508bb-216">Documentation 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-216">Documentation Element (SSDL)</span></span>

<span data-ttu-id="508bb-217">**文档**存储架构定义语言 (SSDL) 中的元素可以用于提供有关的对象的父元素中定义的信息。</span><span class="sxs-lookup"><span data-stu-id="508bb-217">The **Documentation** element in store schema definition language (SSDL) can be used to provide information about an object that is defined in a parent element.</span></span>

<span data-ttu-id="508bb-218">**文档**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-218">The **Documentation** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-219">**摘要**： 父元素的简要说明。</span><span class="sxs-lookup"><span data-stu-id="508bb-219">**Summary**: A brief description of the parent element.</span></span> <span data-ttu-id="508bb-220">（零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-220">(zero or one element)</span></span>
-   <span data-ttu-id="508bb-221">**LongDescription**： 父元素的详细说明。</span><span class="sxs-lookup"><span data-stu-id="508bb-221">**LongDescription**: An extensive description of the parent element.</span></span> <span data-ttu-id="508bb-222">（零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-222">(zero or one element)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-223">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-223">Applicable Attributes</span></span>

<span data-ttu-id="508bb-224">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**文档**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-224">Any number of annotation attributes (custom XML attributes) may be applied to the **Documentation** element.</span></span> <span data-ttu-id="508bb-225">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-225">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="508bb-226">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-226">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-227">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-227">Example</span></span>

<span data-ttu-id="508bb-228">下面的示例演示**文档**元素作为 EntityType 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-228">The following example shows the **Documentation** element as a child element of an EntityType element.</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```

## <a name="end-element-ssdl"></a><span data-ttu-id="508bb-229">End 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-229">End Element (SSDL)</span></span>

<span data-ttu-id="508bb-230">**最终**存储架构定义语言 (SSDL) 中的元素与基础数据库中指定的表和外键约束一端的行数。</span><span class="sxs-lookup"><span data-stu-id="508bb-230">The **End** element in store schema definition language (SSDL) specifies the table and number of rows at one end of a foreign key constraint in the underlying database.</span></span> <span data-ttu-id="508bb-231">**最终**元素可以是 Association 元素或 AssociationSet 元素的子级。</span><span class="sxs-lookup"><span data-stu-id="508bb-231">The **End** element can be a child of the Association element or the AssociationSet element.</span></span> <span data-ttu-id="508bb-232">在每种情况下，可能的子元素以及适用的特性都不同。</span><span class="sxs-lookup"><span data-stu-id="508bb-232">In each case, the possible child elements and applicable attributes are different.</span></span>

### <a name="end-element-as-a-child-of-the-association-element"></a><span data-ttu-id="508bb-233">End 元素作为 Association 元素的子元素</span><span class="sxs-lookup"><span data-stu-id="508bb-233">End Element as a Child of the Association Element</span></span>

<span data-ttu-id="508bb-234">**最终**元素 (作为子级**关联**元素) 指定的表和外键约束与结尾处的行数**类型**和**多重性**分别属性。</span><span class="sxs-lookup"><span data-stu-id="508bb-234">An **End** element (as a child of the **Association** element) specifies the table and number of rows at the end of a foreign key constraint with the **Type** and **Multiplicity** attributes respectively.</span></span> <span data-ttu-id="508bb-235">外键约束的两端定义为 SSDL 关联的一部分；SSDL 关联必须仅具有两端。</span><span class="sxs-lookup"><span data-stu-id="508bb-235">Ends of a foreign key constraint are defined as part of an SSDL association; an SSDL association must have exactly two ends.</span></span>

<span data-ttu-id="508bb-236">**最终**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-236">An **End** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-237">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-237">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="508bb-238">OnDelete （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-238">OnDelete (zero or one element)</span></span>
-   <span data-ttu-id="508bb-239">批注元素 （零个或多个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-239">Annotation elements (zero or more elements)</span></span>

#### <a name="applicable-attributes"></a><span data-ttu-id="508bb-240">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-240">Applicable Attributes</span></span>

<span data-ttu-id="508bb-241">下表介绍可应用于的特性**最终**时的子元素**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-241">The following table describes the attributes that can be applied to the **End** element when it is the child of an **Association** element.</span></span>

| <span data-ttu-id="508bb-242">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-242">Attribute Name</span></span>   | <span data-ttu-id="508bb-243">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-243">Is Required</span></span> | <span data-ttu-id="508bb-244">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-244">Value</span></span>                                                                                                                                                                                                                                                                                                                                                                                      |
|:-----------------|:------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-245">**Type**</span><span class="sxs-lookup"><span data-stu-id="508bb-245">**Type**</span></span>         | <span data-ttu-id="508bb-246">是</span><span class="sxs-lookup"><span data-stu-id="508bb-246">Yes</span></span>         | <span data-ttu-id="508bb-247">在外键约束的末尾处的 SSDL 实体集的完全限定的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-247">The fully qualified name of the SSDL entity set that is at the end of the foreign key constraint.</span></span>                                                                                                                                                                                                                                                                                          |
| <span data-ttu-id="508bb-248">**角色**</span><span class="sxs-lookup"><span data-stu-id="508bb-248">**Role**</span></span>         | <span data-ttu-id="508bb-249">否</span><span class="sxs-lookup"><span data-stu-id="508bb-249">No</span></span>          | <span data-ttu-id="508bb-250">值**角色**属性中的主体或依赖于元素的相应 ReferentialConstraint 元素 （如果使用）。</span><span class="sxs-lookup"><span data-stu-id="508bb-250">The value of the **Role** attribute in either the Principal or Dependent element of the corresponding ReferentialConstraint element (if used).</span></span>                                                                                                                                                                                                                                             |
| <span data-ttu-id="508bb-251">**重数**</span><span class="sxs-lookup"><span data-stu-id="508bb-251">**Multiplicity**</span></span> | <span data-ttu-id="508bb-252">是</span><span class="sxs-lookup"><span data-stu-id="508bb-252">Yes</span></span>         | <span data-ttu-id="508bb-253">**1**， **0..1**，或**\*** 具体取决于外键约束一端可以存在的行数。</span><span class="sxs-lookup"><span data-stu-id="508bb-253">**1**, **0..1**, or **\*** depending on the number of rows that can be at the end of the foreign key constraint.</span></span> <br/> <span data-ttu-id="508bb-254">**1**指示外键约束端处存在恰好一个行。</span><span class="sxs-lookup"><span data-stu-id="508bb-254">**1** indicates that exactly one row exists at the foreign key constraint end.</span></span> <br/> <span data-ttu-id="508bb-255">**0..1**指示外键约束端处存在零个或一个行。</span><span class="sxs-lookup"><span data-stu-id="508bb-255">**0..1** indicates that zero or one row exists at the foreign key constraint end.</span></span> <br/> <span data-ttu-id="508bb-256">**\*** 指示外键约束端处存在零、 一个或多个行。</span><span class="sxs-lookup"><span data-stu-id="508bb-256">**\*** indicates that zero, one, or more rows exist at the foreign key constraint end.</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-257">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**最终**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-257">Any number of annotation attributes (custom XML attributes) may be applied to the **End** element.</span></span> <span data-ttu-id="508bb-258">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-258">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="508bb-259">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-259">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

#### <a name="example"></a><span data-ttu-id="508bb-260">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-260">Example</span></span>

<span data-ttu-id="508bb-261">下面的示例演示**关联**定义的元素**FK\_CustomerOrders**外键约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-261">The following example shows an **Association** element that defines the **FK\_CustomerOrders** foreign key constraint.</span></span> <span data-ttu-id="508bb-262">**多重性**上每个指定值**最终**元素指示中的多行**订单**表可以与中的行相关联**客户**表中，但中的仅有一行**客户**表可以与中的行相关联**订单**表。</span><span class="sxs-lookup"><span data-stu-id="508bb-262">The **Multiplicity** values specified on each **End** element indicate that many rows in the **Orders** table can be associated with a row in the **Customers** table, but only one row in the **Customers** table can be associated with a row in the **Orders** table.</span></span> <span data-ttu-id="508bb-263">此外， **OnDelete**元素指示的所有行中**订单**引用中的特定行的表**客户**如果将删除的表中的行**客户**删除该表。</span><span class="sxs-lookup"><span data-stu-id="508bb-263">Additionally, the **OnDelete** element indicates that all rows in the **Orders** table that reference a particular row in the **Customers** table will be deleted if the row in the **Customers** table is deleted.</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```

### <a name="end-element-as-a-child-of-the-associationset-element"></a><span data-ttu-id="508bb-264">End 元素作为 AssociationSet 元素的子元素</span><span class="sxs-lookup"><span data-stu-id="508bb-264">End Element as a Child of the AssociationSet Element</span></span>

<span data-ttu-id="508bb-265">**最终**元素 (作为子级**AssociationSet**元素) 与基础数据库中指定的外键约束一端的表。</span><span class="sxs-lookup"><span data-stu-id="508bb-265">The **End** element (as a child of the **AssociationSet** element) specifies a table at one end of a foreign key constraint in the underlying database.</span></span>

<span data-ttu-id="508bb-266">**最终**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-266">An **End** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-267">文档 （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-267">Documentation (zero or one)</span></span>
-   <span data-ttu-id="508bb-268">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-268">Annotation elements (zero or more)</span></span>

#### <a name="applicable-attributes"></a><span data-ttu-id="508bb-269">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-269">Applicable Attributes</span></span>

<span data-ttu-id="508bb-270">下表介绍可应用于的特性**最终**时的子元素**AssociationSet**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-270">The following table describes the attributes that can be applied to the **End** element when it is the child of an **AssociationSet** element.</span></span>

| <span data-ttu-id="508bb-271">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-271">Attribute Name</span></span> | <span data-ttu-id="508bb-272">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-272">Is Required</span></span> | <span data-ttu-id="508bb-273">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-273">Value</span></span>                                                                                                                  |
|:---------------|:------------|:-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-274">**实体集**</span><span class="sxs-lookup"><span data-stu-id="508bb-274">**EntitySet**</span></span>  | <span data-ttu-id="508bb-275">是</span><span class="sxs-lookup"><span data-stu-id="508bb-275">Yes</span></span>         | <span data-ttu-id="508bb-276">在外键约束的末尾处的 SSDL 实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-276">The name of the SSDL entity set that is at the end of the foreign key constraint.</span></span>                                      |
| <span data-ttu-id="508bb-277">**角色**</span><span class="sxs-lookup"><span data-stu-id="508bb-277">**Role**</span></span>       | <span data-ttu-id="508bb-278">否</span><span class="sxs-lookup"><span data-stu-id="508bb-278">No</span></span>          | <span data-ttu-id="508bb-279">之一的值**角色**属性指定一个**最终**相应关联元素的元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-279">The value of one of the **Role** attributes specified on one **End** element of the corresponding Association element.</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-280">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**最终**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-280">Any number of annotation attributes (custom XML attributes) may be applied to the **End** element.</span></span> <span data-ttu-id="508bb-281">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-281">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="508bb-282">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-282">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

#### <a name="example"></a><span data-ttu-id="508bb-283">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-283">Example</span></span>

<span data-ttu-id="508bb-284">下面的示例演示**EntityContainer**具有元素**AssociationSet**元素具有两个**最终**元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-284">The following example shows an **EntityContainer** element with an **AssociationSet** element with two **End** elements:</span></span>

``` xml
 <EntityContainer Name="ExampleModelStoreContainer">
   <EntitySet Name="Customers"
              EntityType="ExampleModel.Store.Customers"
              Schema="dbo" />
   <EntitySet Name="Orders"
              EntityType="ExampleModel.Store.Orders"
              Schema="dbo" />
   <AssociationSet Name="FK_CustomerOrders"
                   Association="ExampleModel.Store.FK_CustomerOrders">
     <End Role="Customers" EntitySet="Customers" />
     <End Role="Orders" EntitySet="Orders" />
   </AssociationSet>
 </EntityContainer>
```

## <a name="entitycontainer-element-ssdl"></a><span data-ttu-id="508bb-285">EntityContainer 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-285">EntityContainer Element (SSDL)</span></span>

<span data-ttu-id="508bb-286">**EntityContainer**存储架构定义语言 (SSDL) 中的元素描述中的实体框架应用程序的基础数据源的结构： SSDL 实体集 （在 EntitySet 元素中定义） 表示中的表数据库中，SSDL 实体类型 （EntityType 元素中定义） 表示表中的行和关联集 （在 AssociationSet 元素中定义） 表示在数据库中的外键约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-286">An **EntityContainer** element in store schema definition language (SSDL) describes the structure of the underlying data source in an Entity Framework application: SSDL entity sets (defined in EntitySet elements) represent tables in a database, SSDL entity types (defined in EntityType elements) represent rows in a table, and association sets (defined in AssociationSet elements) represent foreign key constraints in a database.</span></span> <span data-ttu-id="508bb-287">存储模型实体容器映射到概念模型实体容器通过 EntityContainerMapping 元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-287">A storage model entity container maps to a conceptual model entity container through the EntityContainerMapping element.</span></span>

<span data-ttu-id="508bb-288">**EntityContainer**元素可以具有零个或一个文档元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-288">An **EntityContainer** element can have zero or one Documentation elements.</span></span> <span data-ttu-id="508bb-289">如果**文档**元素存在，则它必须位于所有其他子元素之前。</span><span class="sxs-lookup"><span data-stu-id="508bb-289">If a **Documentation** element is present, it must precede all other child elements.</span></span>

<span data-ttu-id="508bb-290">**EntityContainer**元素可以具有零个或多个下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-290">An **EntityContainer** element can have zero or more of the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-291">EntitySet</span><span class="sxs-lookup"><span data-stu-id="508bb-291">EntitySet</span></span>
-   <span data-ttu-id="508bb-292">AssociationSet</span><span class="sxs-lookup"><span data-stu-id="508bb-292">AssociationSet</span></span>
-   <span data-ttu-id="508bb-293">批注元素</span><span class="sxs-lookup"><span data-stu-id="508bb-293">Annotation elements</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-294">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-294">Applicable Attributes</span></span>

<span data-ttu-id="508bb-295">下表描述了可应用于的特性**EntityContainer**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-295">The table below describes the attributes that can be applied to the **EntityContainer** element.</span></span>

| <span data-ttu-id="508bb-296">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-296">Attribute Name</span></span> | <span data-ttu-id="508bb-297">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-297">Is Required</span></span> | <span data-ttu-id="508bb-298">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-298">Value</span></span>                                                                   |
|:---------------|:------------|:------------------------------------------------------------------------|
| <span data-ttu-id="508bb-299">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-299">**Name**</span></span>       | <span data-ttu-id="508bb-300">是</span><span class="sxs-lookup"><span data-stu-id="508bb-300">Yes</span></span>         | <span data-ttu-id="508bb-301">实体容器的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-301">The name of the entity container.</span></span> <span data-ttu-id="508bb-302">此名称不能包含句点 (.)。</span><span class="sxs-lookup"><span data-stu-id="508bb-302">This name cannot contain periods (.).</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-303">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**EntityContainer**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-303">Any number of annotation attributes (custom XML attributes) may be applied to the **EntityContainer** element.</span></span> <span data-ttu-id="508bb-304">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-304">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-305">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-305">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-306">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-306">Example</span></span>

<span data-ttu-id="508bb-307">下面的示例演示**EntityContainer**定义两个实体集和一个关联集的元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-307">The following example shows an **EntityContainer** element that defines two entity sets and one association set.</span></span> <span data-ttu-id="508bb-308">注意，实体类型和关联类型名称由概念模型命名空间名称限定。</span><span class="sxs-lookup"><span data-stu-id="508bb-308">Note that entity type and association type names are qualified by the conceptual model namespace name.</span></span>

``` xml
 <EntityContainer Name="ExampleModelStoreContainer">
   <EntitySet Name="Customers"
              EntityType="ExampleModel.Store.Customers"
              Schema="dbo" />
   <EntitySet Name="Orders"
              EntityType="ExampleModel.Store.Orders"
              Schema="dbo" />
   <AssociationSet Name="FK_CustomerOrders"
                   Association="ExampleModel.Store.FK_CustomerOrders">
     <End Role="Customers" EntitySet="Customers" />
     <End Role="Orders" EntitySet="Orders" />
   </AssociationSet>
 </EntityContainer>
```

## <a name="entityset-element-ssdl"></a><span data-ttu-id="508bb-309">EntitySet 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-309">EntitySet Element (SSDL)</span></span>

<span data-ttu-id="508bb-310">**EntitySet**存储架构定义语言 (SSDL) 中的元素表示表或视图基础数据库中的。</span><span class="sxs-lookup"><span data-stu-id="508bb-310">An **EntitySet** element in store schema definition language (SSDL) represents a table or view in the underlying database.</span></span> <span data-ttu-id="508bb-311">SSDL 中的 EntityType 元素表示表或视图中的行。</span><span class="sxs-lookup"><span data-stu-id="508bb-311">An EntityType element in SSDL represents a row in the table or view.</span></span> <span data-ttu-id="508bb-312">**EntityType**的属性**EntitySet**元素指定表示 SSDL 实体集中的行的特定 SSDL 实体类型。</span><span class="sxs-lookup"><span data-stu-id="508bb-312">The **EntityType** attribute of an **EntitySet** element specifies the particular SSDL entity type that represents rows in an SSDL entity set.</span></span> <span data-ttu-id="508bb-313">EntitySetMapping 元素中指定的 CSDL 实体集和 SSDL 实体集之间的映射。</span><span class="sxs-lookup"><span data-stu-id="508bb-313">The mapping between a CSDL entity set and an SSDL entity set is specified in an EntitySetMapping element.</span></span>

<span data-ttu-id="508bb-314">**EntitySet**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-314">The **EntitySet** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-315">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-315">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="508bb-316">DefiningQuery （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-316">DefiningQuery (zero or one element)</span></span>
-   <span data-ttu-id="508bb-317">批注元素</span><span class="sxs-lookup"><span data-stu-id="508bb-317">Annotation elements</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-318">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-318">Applicable Attributes</span></span>

<span data-ttu-id="508bb-319">下表介绍可应用于的特性**EntitySet**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-319">The following table describes the attributes that can be applied to the **EntitySet** element.</span></span>

> [!NOTE]
> <span data-ttu-id="508bb-320">（此处未列出） 的某些属性可能会用限定**存储**别名。</span><span class="sxs-lookup"><span data-stu-id="508bb-320">Some attributes (not listed here) may be qualified with the **store** alias.</span></span> <span data-ttu-id="508bb-321">模型更新向导更新模型时使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="508bb-321">These attributes are used by the Update Model Wizard when updating a model.</span></span>

| <span data-ttu-id="508bb-322">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-322">Attribute Name</span></span> | <span data-ttu-id="508bb-323">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-323">Is Required</span></span> | <span data-ttu-id="508bb-324">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-324">Value</span></span>                                                                                    |
|:---------------|:------------|:-----------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-325">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-325">**Name**</span></span>       | <span data-ttu-id="508bb-326">是</span><span class="sxs-lookup"><span data-stu-id="508bb-326">Yes</span></span>         | <span data-ttu-id="508bb-327">实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-327">The name of the entity set.</span></span>                                                              |
| <span data-ttu-id="508bb-328">**EntityType**</span><span class="sxs-lookup"><span data-stu-id="508bb-328">**EntityType**</span></span> | <span data-ttu-id="508bb-329">是</span><span class="sxs-lookup"><span data-stu-id="508bb-329">Yes</span></span>         | <span data-ttu-id="508bb-330">实体集包含其实例的实体类型的完全限定名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-330">The fully-qualified name of the entity type for which the entity set contains instances.</span></span> |
| <span data-ttu-id="508bb-331">**架构**</span><span class="sxs-lookup"><span data-stu-id="508bb-331">**Schema**</span></span>     | <span data-ttu-id="508bb-332">否</span><span class="sxs-lookup"><span data-stu-id="508bb-332">No</span></span>          | <span data-ttu-id="508bb-333">数据库架构。</span><span class="sxs-lookup"><span data-stu-id="508bb-333">The database schema.</span></span>                                                                     |
| <span data-ttu-id="508bb-334">**Table**</span><span class="sxs-lookup"><span data-stu-id="508bb-334">**Table**</span></span>      | <span data-ttu-id="508bb-335">否</span><span class="sxs-lookup"><span data-stu-id="508bb-335">No</span></span>          | <span data-ttu-id="508bb-336">数据库表。</span><span class="sxs-lookup"><span data-stu-id="508bb-336">The database table.</span></span>                                                                      |

> [!NOTE]
> <span data-ttu-id="508bb-337">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**EntitySet**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-337">Any number of annotation attributes (custom XML attributes) may be applied to the **EntitySet** element.</span></span> <span data-ttu-id="508bb-338">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-338">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-339">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-339">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-340">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-340">Example</span></span>

<span data-ttu-id="508bb-341">下面的示例演示**EntityContainer**元素具有两个**EntitySet**元素和一个**AssociationSet**元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-341">The following example shows an **EntityContainer** element that has two **EntitySet** elements and one **AssociationSet** element:</span></span>

``` xml
 <EntityContainer Name="ExampleModelStoreContainer">
   <EntitySet Name="Customers"
              EntityType="ExampleModel.Store.Customers"
              Schema="dbo" />
   <EntitySet Name="Orders"
              EntityType="ExampleModel.Store.Orders"
              Schema="dbo" />
   <AssociationSet Name="FK_CustomerOrders"
                   Association="ExampleModel.Store.FK_CustomerOrders">
     <End Role="Customers" EntitySet="Customers" />
     <End Role="Orders" EntitySet="Orders" />
   </AssociationSet>
 </EntityContainer>
```

## <a name="entitytype-element-ssdl"></a><span data-ttu-id="508bb-342">EntityType 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-342">EntityType Element (SSDL)</span></span>

<span data-ttu-id="508bb-343">**EntityType**存储架构定义语言 (SSDL) 中的元素表示表或视图的基础数据库中的行。</span><span class="sxs-lookup"><span data-stu-id="508bb-343">An **EntityType** element in store schema definition language (SSDL) represents a row in a table or view of the underlying database.</span></span> <span data-ttu-id="508bb-344">SSDL 中的 EntitySet 元素表示表或视图，其中出现行。</span><span class="sxs-lookup"><span data-stu-id="508bb-344">An EntitySet element in SSDL represents the table or view in which rows occur.</span></span> <span data-ttu-id="508bb-345">**EntityType**的属性**EntitySet**元素指定表示 SSDL 实体集中的行的特定 SSDL 实体类型。</span><span class="sxs-lookup"><span data-stu-id="508bb-345">The **EntityType** attribute of an **EntitySet** element specifies the particular SSDL entity type that represents rows in an SSDL entity set.</span></span> <span data-ttu-id="508bb-346">EntityTypeMapping 元素中指定的 SSDL 实体类型和 CSDL 实体类型之间的映射。</span><span class="sxs-lookup"><span data-stu-id="508bb-346">The mapping between an SSDL entity type and a CSDL entity type is specified in an EntityTypeMapping element.</span></span>

<span data-ttu-id="508bb-347">**EntityType**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-347">The **EntityType** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-348">文档 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-348">Documentation (zero or one element)</span></span>
-   <span data-ttu-id="508bb-349">密钥 （零个或一个元素）</span><span class="sxs-lookup"><span data-stu-id="508bb-349">Key (zero or one element)</span></span>
-   <span data-ttu-id="508bb-350">批注元素</span><span class="sxs-lookup"><span data-stu-id="508bb-350">Annotation elements</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-351">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-351">Applicable Attributes</span></span>

<span data-ttu-id="508bb-352">下表描述了可应用于的特性**EntityType**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-352">The table below describes the attributes that can be applied to the **EntityType** element.</span></span>

| <span data-ttu-id="508bb-353">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-353">Attribute Name</span></span> | <span data-ttu-id="508bb-354">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-354">Is Required</span></span> | <span data-ttu-id="508bb-355">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-355">Value</span></span>                                                                                                                                                                  |
|:---------------|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-356">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-356">**Name**</span></span>       | <span data-ttu-id="508bb-357">是</span><span class="sxs-lookup"><span data-stu-id="508bb-357">Yes</span></span>         | <span data-ttu-id="508bb-358">实体类型的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-358">The name of the entity type.</span></span> <span data-ttu-id="508bb-359">此值通常与以实体类型表示行的表的名称相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-359">This value is usually the same as the name of the table in which the entity type represents a row.</span></span> <span data-ttu-id="508bb-360">此值可以不包含句点 (.)。</span><span class="sxs-lookup"><span data-stu-id="508bb-360">This value can contain no periods (.).</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-361">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**EntityType**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-361">Any number of annotation attributes (custom XML attributes) may be applied to the **EntityType** element.</span></span> <span data-ttu-id="508bb-362">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-362">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-363">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-363">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-364">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-364">Example</span></span>

<span data-ttu-id="508bb-365">下面的示例演示**EntityType**元素具有两个属性：</span><span class="sxs-lookup"><span data-stu-id="508bb-365">The following example shows an **EntityType** element with two properties:</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```

## <a name="function-element-ssdl"></a><span data-ttu-id="508bb-366">Function 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-366">Function Element (SSDL)</span></span>

<span data-ttu-id="508bb-367">**函数**存储架构定义语言 (SSDL) 中的元素指定基础数据库中存在的存储的过程。</span><span class="sxs-lookup"><span data-stu-id="508bb-367">The **Function** element in store schema definition language (SSDL) specifies a stored procedure that exists in the underlying database.</span></span>

<span data-ttu-id="508bb-368">**函数**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-368">The **Function** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-369">文档 （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-369">Documentation (zero or one)</span></span>
-   <span data-ttu-id="508bb-370">参数 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-370">Parameter (zero or more)</span></span>
-   <span data-ttu-id="508bb-371">CommandText （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-371">CommandText (zero or one)</span></span>
-   <span data-ttu-id="508bb-372">ReturnType （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-372">ReturnType (zero or more)</span></span>
-   <span data-ttu-id="508bb-373">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-373">Annotation elements (zero or more)</span></span>

<span data-ttu-id="508bb-374">返回类型的函数必须指定与**ReturnType**元素或**ReturnType**属性 （见下文），但不可同时使用两者。</span><span class="sxs-lookup"><span data-stu-id="508bb-374">A return type for a function must be specified with either the **ReturnType** element or the **ReturnType** attribute (see below), but not both.</span></span>

<span data-ttu-id="508bb-375">可以将在存储模型中指定的存储过程导入应用程序的概念模型。</span><span class="sxs-lookup"><span data-stu-id="508bb-375">Stored procedures that are specified in the storage model can be imported into the conceptual model of an application.</span></span> <span data-ttu-id="508bb-376">有关详细信息，请参阅[存储过程使用查询](~/ef6/modeling/designer/stored-procedures/query.md)。</span><span class="sxs-lookup"><span data-stu-id="508bb-376">For more information, see [Querying with Stored Procedures](~/ef6/modeling/designer/stored-procedures/query.md).</span></span> <span data-ttu-id="508bb-377">**函数**元素还可用于在存储模型中定义自定义函数。</span><span class="sxs-lookup"><span data-stu-id="508bb-377">The **Function** element can also be used to define custom functions in the storage model.</span></span>  

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-378">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-378">Applicable Attributes</span></span>

<span data-ttu-id="508bb-379">下表介绍可应用于的特性**函数**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-379">The following table describes the attributes that can be applied to the **Function** element.</span></span>

> [!NOTE]
> <span data-ttu-id="508bb-380">（此处未列出） 的某些属性可能会用限定**存储**别名。</span><span class="sxs-lookup"><span data-stu-id="508bb-380">Some attributes (not listed here) may be qualified with the **store** alias.</span></span> <span data-ttu-id="508bb-381">模型更新向导更新模型时使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="508bb-381">These attributes are used by the Update Model Wizard when updating a model.</span></span>

| <span data-ttu-id="508bb-382">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-382">Attribute Name</span></span>             | <span data-ttu-id="508bb-383">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-383">Is Required</span></span> | <span data-ttu-id="508bb-384">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-384">Value</span></span>                                                                                                                                                                                                              |
|:---------------------------|:------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-385">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-385">**Name**</span></span>                   | <span data-ttu-id="508bb-386">是</span><span class="sxs-lookup"><span data-stu-id="508bb-386">Yes</span></span>         | <span data-ttu-id="508bb-387">存储过程的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-387">The name of the stored procedure.</span></span>                                                                                                                                                                                  |
| <span data-ttu-id="508bb-388">**ReturnType**</span><span class="sxs-lookup"><span data-stu-id="508bb-388">**ReturnType**</span></span>             | <span data-ttu-id="508bb-389">否</span><span class="sxs-lookup"><span data-stu-id="508bb-389">No</span></span>          | <span data-ttu-id="508bb-390">存储过程的返回类型。</span><span class="sxs-lookup"><span data-stu-id="508bb-390">The return type of the stored procedure.</span></span>                                                                                                                                                                           |
| <span data-ttu-id="508bb-391">**Aggregate**</span><span class="sxs-lookup"><span data-stu-id="508bb-391">**Aggregate**</span></span>              | <span data-ttu-id="508bb-392">否</span><span class="sxs-lookup"><span data-stu-id="508bb-392">No</span></span>          | <span data-ttu-id="508bb-393">**True**如果存储的过程返回的聚合值; 否则为**False**。</span><span class="sxs-lookup"><span data-stu-id="508bb-393">**True** if the stored procedure returns an aggregate value; otherwise **False**.</span></span>                                                                                                                                  |
| <span data-ttu-id="508bb-394">**内置**</span><span class="sxs-lookup"><span data-stu-id="508bb-394">**BuiltIn**</span></span>                | <span data-ttu-id="508bb-395">否</span><span class="sxs-lookup"><span data-stu-id="508bb-395">No</span></span>          | <span data-ttu-id="508bb-396">**True**如果函数为内置<sup>1</sup>函数; 否则为**False**。</span><span class="sxs-lookup"><span data-stu-id="508bb-396">**True** if the function is a built-in<sup>1</sup> function; otherwise **False**.</span></span>                                                                                                                                  |
| <span data-ttu-id="508bb-397">**StoreFunctionName**</span><span class="sxs-lookup"><span data-stu-id="508bb-397">**StoreFunctionName**</span></span>      | <span data-ttu-id="508bb-398">否</span><span class="sxs-lookup"><span data-stu-id="508bb-398">No</span></span>          | <span data-ttu-id="508bb-399">存储过程的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-399">The name of the stored procedure.</span></span>                                                                                                                                                                                  |
| <span data-ttu-id="508bb-400">**NiladicFunction**</span><span class="sxs-lookup"><span data-stu-id="508bb-400">**NiladicFunction**</span></span>        | <span data-ttu-id="508bb-401">否</span><span class="sxs-lookup"><span data-stu-id="508bb-401">No</span></span>          | <span data-ttu-id="508bb-402">**True**如果函数为 niladic<sup>2</sup>函数;**False**否则为。</span><span class="sxs-lookup"><span data-stu-id="508bb-402">**True** if the function is a niladic<sup>2</sup> function; **False** otherwise.</span></span>                                                                                                                                   |
| <span data-ttu-id="508bb-403">**IsComposable**</span><span class="sxs-lookup"><span data-stu-id="508bb-403">**IsComposable**</span></span>           | <span data-ttu-id="508bb-404">否</span><span class="sxs-lookup"><span data-stu-id="508bb-404">No</span></span>          | <span data-ttu-id="508bb-405">**True**如果该函数是可组合<sup>3</sup>函数;**False**否则为。</span><span class="sxs-lookup"><span data-stu-id="508bb-405">**True** if the function is a composable<sup>3</sup> function; **False** otherwise.</span></span>                                                                                                                                |
| <span data-ttu-id="508bb-406">**ParameterTypeSemantics**</span><span class="sxs-lookup"><span data-stu-id="508bb-406">**ParameterTypeSemantics**</span></span> | <span data-ttu-id="508bb-407">否</span><span class="sxs-lookup"><span data-stu-id="508bb-407">No</span></span>          | <span data-ttu-id="508bb-408">定义用于解析函数重载的类型语义的枚举。</span><span class="sxs-lookup"><span data-stu-id="508bb-408">The enumeration that defines the type semantics used to resolve function overloads.</span></span> <span data-ttu-id="508bb-409">该枚举是在提供程序清单中根据函数定义来定义的。</span><span class="sxs-lookup"><span data-stu-id="508bb-409">The enumeration is defined in the provider manifest per function definition.</span></span> <span data-ttu-id="508bb-410">默认值是**AllowImplicitConversion**。</span><span class="sxs-lookup"><span data-stu-id="508bb-410">The default value is **AllowImplicitConversion**.</span></span> |
| <span data-ttu-id="508bb-411">**架构**</span><span class="sxs-lookup"><span data-stu-id="508bb-411">**Schema**</span></span>                 | <span data-ttu-id="508bb-412">否</span><span class="sxs-lookup"><span data-stu-id="508bb-412">No</span></span>          | <span data-ttu-id="508bb-413">在其中定义存储过程的架构的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-413">The name of the schema in which the stored procedure is defined.</span></span>                                                                                                                                                   |

<span data-ttu-id="508bb-414"><sup>1</sup>内置函数是在数据库中定义的函数。</span><span class="sxs-lookup"><span data-stu-id="508bb-414"><sup>1</sup> A built-in function is a function that is defined in the database.</span></span> <span data-ttu-id="508bb-415">有关存储模型中定义的函数的信息，请参阅 CommandText 元素 (SSDL)。</span><span class="sxs-lookup"><span data-stu-id="508bb-415">For information about functions that are defined in the storage model, see CommandText Element (SSDL).</span></span>

<span data-ttu-id="508bb-416"><sup>2</sup> niladic 函数是不接受任何参数，并调用时，不需要使用括号的函数。</span><span class="sxs-lookup"><span data-stu-id="508bb-416"><sup>2</sup> A niladic function is a function that accepts no parameters and, when called, does not require parentheses.</span></span>

<span data-ttu-id="508bb-417"><sup>3</sup>两个函数是可组合，如果一个函数的输出可以是其他函数的输入。</span><span class="sxs-lookup"><span data-stu-id="508bb-417"><sup>3</sup> Two functions are composable if the output of one function can be the input for the other function.</span></span>

> [!NOTE]
> <span data-ttu-id="508bb-418">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**函数**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-418">Any number of annotation attributes (custom XML attributes) may be applied to the **Function** element.</span></span> <span data-ttu-id="508bb-419">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-419">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-420">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-420">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-421">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-421">Example</span></span>

<span data-ttu-id="508bb-422">下面的示例演示**函数**对应的元素**UpdateOrderQuantity**存储过程。</span><span class="sxs-lookup"><span data-stu-id="508bb-422">The following example shows a **Function** element that corresponds to the **UpdateOrderQuantity** stored procedure.</span></span> <span data-ttu-id="508bb-423">该存储过程接受两个参数，且不返回值。</span><span class="sxs-lookup"><span data-stu-id="508bb-423">The stored procedure accepts two parameters and does not return a value.</span></span>

``` xml
 <Function Name="UpdateOrderQuantity"
           Aggregate="false"
           BuiltIn="false"
           NiladicFunction="false"
           IsComposable="false"
           ParameterTypeSemantics="AllowImplicitConversion"
           Schema="dbo">
   <Parameter Name="orderId" Type="int" Mode="In" />
   <Parameter Name="newQuantity" Type="int" Mode="In" />
 </Function>
```

## <a name="key-element-ssdl"></a><span data-ttu-id="508bb-424">Key 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-424">Key Element (SSDL)</span></span>

<span data-ttu-id="508bb-425">**密钥**存储架构定义语言 (SSDL) 中的元素表示基础数据库中的表的主键。</span><span class="sxs-lookup"><span data-stu-id="508bb-425">The **Key** element in store schema definition language (SSDL) represents the primary key of a table in the underlying database.</span></span> <span data-ttu-id="508bb-426">**密钥**是 EntityType 元素，它表示表中的行的子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-426">**Key** is a child element of an EntityType element, which represents a row in a table.</span></span> <span data-ttu-id="508bb-427">在中定义的主键**键**通过引用一个或多个属性元素上定义的元素**EntityType**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-427">The primary key is defined in the **Key** element by referencing one or more Property elements that are defined on the **EntityType** element.</span></span>

<span data-ttu-id="508bb-428">**密钥**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-428">The **Key** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-429">PropertyRef （一个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-429">PropertyRef (one or more)</span></span>
-   <span data-ttu-id="508bb-430">批注元素</span><span class="sxs-lookup"><span data-stu-id="508bb-430">Annotation elements</span></span>

<span data-ttu-id="508bb-431">任何属性都适用于**密钥**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-431">No attributes are applicable to the **Key** element.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-432">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-432">Example</span></span>

<span data-ttu-id="508bb-433">下面的示例演示**EntityType**具有引用一个属性的键的元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-433">The following example shows an **EntityType** element with a key that references one property:</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```

## <a name="ondelete-element-ssdl"></a><span data-ttu-id="508bb-434">OnDelete 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-434">OnDelete Element (SSDL)</span></span>

<span data-ttu-id="508bb-435">**OnDelete**删除参与外键约束的行时，存储架构定义语言 (SSDL) 中的元素反映数据库的行为。</span><span class="sxs-lookup"><span data-stu-id="508bb-435">The **OnDelete** element in store schema definition language (SSDL) reflects the database behavior when a row that participates in a foreign key constraint is deleted.</span></span> <span data-ttu-id="508bb-436">如果将操作设置为**Cascade**，则还将删除引用要删除的行的行。</span><span class="sxs-lookup"><span data-stu-id="508bb-436">If the action is set to **Cascade**, then rows that reference a row that is being deleted will also be deleted.</span></span> <span data-ttu-id="508bb-437">如果将操作设置为**None**，然后引用要删除的行的行也不会删除。</span><span class="sxs-lookup"><span data-stu-id="508bb-437">If the action is set to **None**, then rows that reference a row that is being deleted are not also deleted.</span></span> <span data-ttu-id="508bb-438">**OnDelete**元素是子元素的结束元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-438">An **OnDelete** element is a child element of an End element.</span></span>

<span data-ttu-id="508bb-439">**OnDelete**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-439">An **OnDelete** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-440">文档 （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-440">Documentation (zero or one)</span></span>
-   <span data-ttu-id="508bb-441">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-441">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-442">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-442">Applicable Attributes</span></span>

<span data-ttu-id="508bb-443">下表介绍可应用于的特性**OnDelete**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-443">The following table describes the attributes that can be applied to the **OnDelete** element.</span></span>

| <span data-ttu-id="508bb-444">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-444">Attribute Name</span></span> | <span data-ttu-id="508bb-445">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-445">Is Required</span></span> | <span data-ttu-id="508bb-446">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-446">Value</span></span>                                                                                               |
|:---------------|:------------|:----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-447">**操作**</span><span class="sxs-lookup"><span data-stu-id="508bb-447">**Action**</span></span>     | <span data-ttu-id="508bb-448">是</span><span class="sxs-lookup"><span data-stu-id="508bb-448">Yes</span></span>         | <span data-ttu-id="508bb-449">**级联**或**None**。</span><span class="sxs-lookup"><span data-stu-id="508bb-449">**Cascade** or **None**.</span></span> <span data-ttu-id="508bb-450">(该值**Restricted**有效，但具有相同的行为**None**。)</span><span class="sxs-lookup"><span data-stu-id="508bb-450">(The value **Restricted** is valid but has the same behavior as **None**.)</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-451">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**OnDelete**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-451">Any number of annotation attributes (custom XML attributes) may be applied to the **OnDelete** element.</span></span> <span data-ttu-id="508bb-452">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-452">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-453">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-453">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-454">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-454">Example</span></span>

<span data-ttu-id="508bb-455">下面的示例演示**关联**定义的元素**FK\_CustomerOrders**外键约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-455">The following example shows an **Association** element that defines the **FK\_CustomerOrders** foreign key constraint.</span></span> <span data-ttu-id="508bb-456">**OnDelete**元素指示的所有行中**订单**引用中的特定行的表**客户**将删除的表，如果中行**客户**删除该表。</span><span class="sxs-lookup"><span data-stu-id="508bb-456">The **OnDelete** element indicates that all rows in the **Orders** table that reference a particular row in the **Customers** table will be deleted if the row in the **Customers** table is deleted.</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```

## <a name="parameter-element-ssdl"></a><span data-ttu-id="508bb-457">Parameter 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-457">Parameter Element (SSDL)</span></span>

<span data-ttu-id="508bb-458">**参数**存储架构定义语言 (SSDL) 中的元素是指定数据库中的存储过程参数的函数元素的子级。</span><span class="sxs-lookup"><span data-stu-id="508bb-458">The **Parameter** element in store schema definition language (SSDL) is a child of the Function element that specifies parameters for a stored procedure in the database.</span></span>

<span data-ttu-id="508bb-459">**参数**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-459">The **Parameter** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-460">文档 （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-460">Documentation (zero or one)</span></span>
-   <span data-ttu-id="508bb-461">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-461">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-462">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-462">Applicable Attributes</span></span>

<span data-ttu-id="508bb-463">下表描述了可应用于的特性**参数**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-463">The table below describes the attributes that can be applied to the **Parameter** element.</span></span>

| <span data-ttu-id="508bb-464">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-464">Attribute Name</span></span> | <span data-ttu-id="508bb-465">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-465">Is Required</span></span> | <span data-ttu-id="508bb-466">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-466">Value</span></span>                                                                                                                                                                                                                           |
|:---------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-467">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-467">**Name**</span></span>       | <span data-ttu-id="508bb-468">是</span><span class="sxs-lookup"><span data-stu-id="508bb-468">Yes</span></span>         | <span data-ttu-id="508bb-469">参数的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-469">The name of the parameter.</span></span>                                                                                                                                                                                                      |
| <span data-ttu-id="508bb-470">**Type**</span><span class="sxs-lookup"><span data-stu-id="508bb-470">**Type**</span></span>       | <span data-ttu-id="508bb-471">是</span><span class="sxs-lookup"><span data-stu-id="508bb-471">Yes</span></span>         | <span data-ttu-id="508bb-472">参数类型。</span><span class="sxs-lookup"><span data-stu-id="508bb-472">The parameter type.</span></span>                                                                                                                                                                                                             |
| <span data-ttu-id="508bb-473">**模式**</span><span class="sxs-lookup"><span data-stu-id="508bb-473">**Mode**</span></span>       | <span data-ttu-id="508bb-474">否</span><span class="sxs-lookup"><span data-stu-id="508bb-474">No</span></span>          | <span data-ttu-id="508bb-475">**在中**，**出**，或**InOut**具体取决于参数是输入、 输出或输入/输出参数。</span><span class="sxs-lookup"><span data-stu-id="508bb-475">**In**, **Out**, or **InOut** depending on whether the parameter is an input, output, or input/output parameter.</span></span>                                                                                                                |
| <span data-ttu-id="508bb-476">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="508bb-476">**MaxLength**</span></span>  | <span data-ttu-id="508bb-477">否</span><span class="sxs-lookup"><span data-stu-id="508bb-477">No</span></span>          | <span data-ttu-id="508bb-478">参数的最大长度。</span><span class="sxs-lookup"><span data-stu-id="508bb-478">The maximum length of the parameter.</span></span>                                                                                                                                                                                            |
| <span data-ttu-id="508bb-479">**精度**</span><span class="sxs-lookup"><span data-stu-id="508bb-479">**Precision**</span></span>  | <span data-ttu-id="508bb-480">否</span><span class="sxs-lookup"><span data-stu-id="508bb-480">No</span></span>          | <span data-ttu-id="508bb-481">参数的精度。</span><span class="sxs-lookup"><span data-stu-id="508bb-481">The precision of the parameter.</span></span>                                                                                                                                                                                                 |
| <span data-ttu-id="508bb-482">缩放</span><span class="sxs-lookup"><span data-stu-id="508bb-482">**Scale**</span></span>      | <span data-ttu-id="508bb-483">否</span><span class="sxs-lookup"><span data-stu-id="508bb-483">No</span></span>          | <span data-ttu-id="508bb-484">参数的小数位数。</span><span class="sxs-lookup"><span data-stu-id="508bb-484">The scale of the parameter.</span></span>                                                                                                                                                                                                     |
| <span data-ttu-id="508bb-485">**SRID**</span><span class="sxs-lookup"><span data-stu-id="508bb-485">**SRID**</span></span>       | <span data-ttu-id="508bb-486">否</span><span class="sxs-lookup"><span data-stu-id="508bb-486">No</span></span>          | <span data-ttu-id="508bb-487">系统的空间引用标识符。</span><span class="sxs-lookup"><span data-stu-id="508bb-487">Spatial System Reference Identifier.</span></span> <span data-ttu-id="508bb-488">仅对空间类型的参数有效。</span><span class="sxs-lookup"><span data-stu-id="508bb-488">Valid only for parameters of spatial types.</span></span> <span data-ttu-id="508bb-489">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)并[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)。</span><span class="sxs-lookup"><span data-stu-id="508bb-489">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-490">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**参数**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-490">Any number of annotation attributes (custom XML attributes) may be applied to the **Parameter** element.</span></span> <span data-ttu-id="508bb-491">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-491">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-492">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-492">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-493">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-493">Example</span></span>

<span data-ttu-id="508bb-494">下面的示例演示**函数**元素具有两个**参数**指定输入的参数的元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-494">The following example shows a **Function** element that has two **Parameter** elements that specify input parameters:</span></span>

``` xml
 <Function Name="UpdateOrderQuantity"
           Aggregate="false"
           BuiltIn="false"
           NiladicFunction="false"
           IsComposable="false"
           ParameterTypeSemantics="AllowImplicitConversion"
           Schema="dbo">
   <Parameter Name="orderId" Type="int" Mode="In" />
   <Parameter Name="newQuantity" Type="int" Mode="In" />
 </Function>
```

## <a name="principal-element-ssdl"></a><span data-ttu-id="508bb-495">Principal 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-495">Principal Element (SSDL)</span></span>

<span data-ttu-id="508bb-496">**主体**存储架构定义语言 (SSDL) 中的元素是定义 （也称为引用约束） 的外键约束的主体端 ReferentialConstraint 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-496">The **Principal** element in store schema definition language (SSDL) is a child element to the ReferentialConstraint element that defines the principal end of a foreign key constraint (also called a referential constraint).</span></span> <span data-ttu-id="508bb-497">**主体**元素引用的另一列 （或列） 的表中指定的主键列 （或列）。</span><span class="sxs-lookup"><span data-stu-id="508bb-497">The **Principal** element specifies the primary key column (or columns) in a table that is referenced by another column (or columns).</span></span> <span data-ttu-id="508bb-498">**PropertyRef**元素指定所引用的列。</span><span class="sxs-lookup"><span data-stu-id="508bb-498">**PropertyRef** elements specify which columns are referenced.</span></span> <span data-ttu-id="508bb-499">Dependent 元素指定引用中指定的主键列的列**主体**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-499">The Dependent element specifies columns that reference the primary key columns that are specified in the **Principal** element.</span></span>

<span data-ttu-id="508bb-500">**主体**元素可以具有下列子元素 （按所列顺序）：</span><span class="sxs-lookup"><span data-stu-id="508bb-500">The **Principal** element can have the following child elements (in the order listed):</span></span>

-   <span data-ttu-id="508bb-501">PropertyRef （一个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-501">PropertyRef (one or more)</span></span>
-   <span data-ttu-id="508bb-502">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-502">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-503">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-503">Applicable Attributes</span></span>

<span data-ttu-id="508bb-504">下表介绍可应用于的特性**主体**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-504">The following table describes the attributes that can be applied to the **Principal** element.</span></span>

| <span data-ttu-id="508bb-505">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-505">Attribute Name</span></span> | <span data-ttu-id="508bb-506">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-506">Is Required</span></span> | <span data-ttu-id="508bb-507">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-507">Value</span></span>                                                                                                                                                      |
|:---------------|:------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-508">**角色**</span><span class="sxs-lookup"><span data-stu-id="508bb-508">**Role**</span></span>       | <span data-ttu-id="508bb-509">是</span><span class="sxs-lookup"><span data-stu-id="508bb-509">Yes</span></span>         | <span data-ttu-id="508bb-510">相同的值**角色**相应的结束元素的特性 （若使用）; 否则为的表的名称包含的被引用的列。</span><span class="sxs-lookup"><span data-stu-id="508bb-510">The same value as the **Role** attribute (if used) of the corresponding End element; otherwise, the name of the table that contains the referenced column.</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-511">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**主体**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-511">Any number of annotation attributes (custom XML attributes) may be applied to the **Principal** element.</span></span> <span data-ttu-id="508bb-512">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-512">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="508bb-513">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-513">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-514">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-514">Example</span></span>

<span data-ttu-id="508bb-515">下面的示例演示使用 Association 元素**ReferentialConstraint**元素指定参与的列**FK\_CustomerOrders**外键约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-515">The following example shows an Association element that uses a **ReferentialConstraint** element to specify the columns that participate in the **FK\_CustomerOrders** foreign key constraint.</span></span> <span data-ttu-id="508bb-516">**主体**元素指定**CustomerId**的列**客户**表约束的主体端。</span><span class="sxs-lookup"><span data-stu-id="508bb-516">The **Principal** element specifies the **CustomerId** column of the **Customer** table as the principal end of the constraint.</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```

## <a name="property-element-ssdl"></a><span data-ttu-id="508bb-517">Property 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-517">Property Element (SSDL)</span></span>

<span data-ttu-id="508bb-518">**属性**存储架构定义语言 (SSDL) 中的元素表示基础数据库中的表中的列。</span><span class="sxs-lookup"><span data-stu-id="508bb-518">The **Property** element in store schema definition language (SSDL) represents a column in a table in the underlying database.</span></span> <span data-ttu-id="508bb-519">**属性**元素是 EntityType 元素，它表示表中的行的子级。</span><span class="sxs-lookup"><span data-stu-id="508bb-519">**Property** elements are children of EntityType elements, which represent rows in a table.</span></span> <span data-ttu-id="508bb-520">每个**属性**元素中定义**EntityType**元素表示的列。</span><span class="sxs-lookup"><span data-stu-id="508bb-520">Each **Property** element defined on an **EntityType** element represents a column.</span></span>

<span data-ttu-id="508bb-521">一个**属性**元素不能具有任何子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-521">A **Property** element cannot have any child elements.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-522">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-522">Applicable Attributes</span></span>

<span data-ttu-id="508bb-523">下表介绍可应用于的特性**属性**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-523">The following table describes the attributes that can be applied to the **Property** element.</span></span>

| <span data-ttu-id="508bb-524">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-524">Attribute Name</span></span>            | <span data-ttu-id="508bb-525">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-525">Is Required</span></span> | <span data-ttu-id="508bb-526">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-526">Value</span></span>                                                                                                                                                                                                                           |
|:--------------------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-527">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-527">**Name**</span></span>                  | <span data-ttu-id="508bb-528">是</span><span class="sxs-lookup"><span data-stu-id="508bb-528">Yes</span></span>         | <span data-ttu-id="508bb-529">对应列的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-529">The name of the corresponding column.</span></span>                                                                                                                                                                                           |
| <span data-ttu-id="508bb-530">**Type**</span><span class="sxs-lookup"><span data-stu-id="508bb-530">**Type**</span></span>                  | <span data-ttu-id="508bb-531">是</span><span class="sxs-lookup"><span data-stu-id="508bb-531">Yes</span></span>         | <span data-ttu-id="508bb-532">对应列的类型。</span><span class="sxs-lookup"><span data-stu-id="508bb-532">The type of the corresponding column.</span></span>                                                                                                                                                                                           |
| <span data-ttu-id="508bb-533">**可以为 null**</span><span class="sxs-lookup"><span data-stu-id="508bb-533">**Nullable**</span></span>              | <span data-ttu-id="508bb-534">否</span><span class="sxs-lookup"><span data-stu-id="508bb-534">No</span></span>          | <span data-ttu-id="508bb-535">**True** （默认值） 或**False**具体取决于相应的列是否可以具有 null 值。</span><span class="sxs-lookup"><span data-stu-id="508bb-535">**True** (the default value) or **False** depending on whether the corresponding column can have a null value.</span></span>                                                                                                                  |
| <span data-ttu-id="508bb-536">**DefaultValue**</span><span class="sxs-lookup"><span data-stu-id="508bb-536">**DefaultValue**</span></span>          | <span data-ttu-id="508bb-537">否</span><span class="sxs-lookup"><span data-stu-id="508bb-537">No</span></span>          | <span data-ttu-id="508bb-538">对应列的默认值。</span><span class="sxs-lookup"><span data-stu-id="508bb-538">The default value of the corresponding column.</span></span>                                                                                                                                                                                  |
| <span data-ttu-id="508bb-539">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="508bb-539">**MaxLength**</span></span>             | <span data-ttu-id="508bb-540">否</span><span class="sxs-lookup"><span data-stu-id="508bb-540">No</span></span>          | <span data-ttu-id="508bb-541">对应列的最大长度。</span><span class="sxs-lookup"><span data-stu-id="508bb-541">The maximum length of the corresponding column.</span></span>                                                                                                                                                                                 |
| <span data-ttu-id="508bb-542">**FixedLength**</span><span class="sxs-lookup"><span data-stu-id="508bb-542">**FixedLength**</span></span>           | <span data-ttu-id="508bb-543">否</span><span class="sxs-lookup"><span data-stu-id="508bb-543">No</span></span>          | <span data-ttu-id="508bb-544">**True**或**False**具体取决于对应列值是否将作为固定的长度字符串存储。</span><span class="sxs-lookup"><span data-stu-id="508bb-544">**True** or **False** depending on whether the corresponding column value will be stored as a fixed length string.</span></span>                                                                                                              |
| <span data-ttu-id="508bb-545">**精度**</span><span class="sxs-lookup"><span data-stu-id="508bb-545">**Precision**</span></span>             | <span data-ttu-id="508bb-546">否</span><span class="sxs-lookup"><span data-stu-id="508bb-546">No</span></span>          | <span data-ttu-id="508bb-547">对应列的精度。</span><span class="sxs-lookup"><span data-stu-id="508bb-547">The precision of the corresponding column.</span></span>                                                                                                                                                                                      |
| <span data-ttu-id="508bb-548">缩放</span><span class="sxs-lookup"><span data-stu-id="508bb-548">**Scale**</span></span>                 | <span data-ttu-id="508bb-549">否</span><span class="sxs-lookup"><span data-stu-id="508bb-549">No</span></span>          | <span data-ttu-id="508bb-550">对应列的小数位数。</span><span class="sxs-lookup"><span data-stu-id="508bb-550">The scale of the corresponding column.</span></span>                                                                                                                                                                                          |
| <span data-ttu-id="508bb-551">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="508bb-551">**Unicode**</span></span>               | <span data-ttu-id="508bb-552">否</span><span class="sxs-lookup"><span data-stu-id="508bb-552">No</span></span>          | <span data-ttu-id="508bb-553">**True**或**False**具体取决于对应列值是否将存储为 Unicode 字符串。</span><span class="sxs-lookup"><span data-stu-id="508bb-553">**True** or **False** depending on whether the corresponding column value will be stored as a Unicode string.</span></span>                                                                                                                   |
| <span data-ttu-id="508bb-554">**排序规则**</span><span class="sxs-lookup"><span data-stu-id="508bb-554">**Collation**</span></span>             | <span data-ttu-id="508bb-555">否</span><span class="sxs-lookup"><span data-stu-id="508bb-555">No</span></span>          | <span data-ttu-id="508bb-556">指定要在数据源中使用的排序序列的字符串。</span><span class="sxs-lookup"><span data-stu-id="508bb-556">A string that specifies the collating sequence to be used in the data source.</span></span>                                                                                                                                                   |
| <span data-ttu-id="508bb-557">**SRID**</span><span class="sxs-lookup"><span data-stu-id="508bb-557">**SRID**</span></span>                  | <span data-ttu-id="508bb-558">否</span><span class="sxs-lookup"><span data-stu-id="508bb-558">No</span></span>          | <span data-ttu-id="508bb-559">系统的空间引用标识符。</span><span class="sxs-lookup"><span data-stu-id="508bb-559">Spatial System Reference Identifier.</span></span> <span data-ttu-id="508bb-560">仅对空间类型的属性有效。</span><span class="sxs-lookup"><span data-stu-id="508bb-560">Valid only for properties of spatial types.</span></span> <span data-ttu-id="508bb-561">有关详细信息，请参阅[SRID](http://en.wikipedia.org/wiki/SRID)并[SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx)。</span><span class="sxs-lookup"><span data-stu-id="508bb-561">For more information, see [SRID](http://en.wikipedia.org/wiki/SRID) and [SRID (SQL Server)](https://msdn.microsoft.com/library/bb964707.aspx).</span></span> |
| <span data-ttu-id="508bb-562">**StoreGeneratedPattern**</span><span class="sxs-lookup"><span data-stu-id="508bb-562">**StoreGeneratedPattern**</span></span> | <span data-ttu-id="508bb-563">否</span><span class="sxs-lookup"><span data-stu-id="508bb-563">No</span></span>          | <span data-ttu-id="508bb-564">**无**，**标识**（如果对应列值为数据库中生成的标识），或**计算**（如果相应列计算的值是在数据库中）。</span><span class="sxs-lookup"><span data-stu-id="508bb-564">**None**, **Identity** (if the corresponding column value is an identity that is generated in the database), or **Computed** (if the corresponding column value is computed in the database).</span></span> <span data-ttu-id="508bb-565">不是有效行类型属性。</span><span class="sxs-lookup"><span data-stu-id="508bb-565">Not Valid for RowType properties.</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-566">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**属性**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-566">Any number of annotation attributes (custom XML attributes) may be applied to the **Property** element.</span></span> <span data-ttu-id="508bb-567">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-567">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-568">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-568">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-569">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-569">Example</span></span>

<span data-ttu-id="508bb-570">下面的示例演示**EntityType**具有两个子元素**属性**元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-570">The following example shows an **EntityType** element with two child **Property** elements:</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```

## <a name="propertyref-element-ssdl"></a><span data-ttu-id="508bb-571">PropertyRef 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-571">PropertyRef Element (SSDL)</span></span>

<span data-ttu-id="508bb-572">**PropertyRef**存储架构定义语言 (SSDL) 中的元素引用以指示该属性将承担以下角色之一的 EntityType 元素上定义的属性：</span><span class="sxs-lookup"><span data-stu-id="508bb-572">The **PropertyRef** element in store schema definition language (SSDL) references a property defined on an EntityType element to indicate that the property will perform one of the following roles:</span></span>

-   <span data-ttu-id="508bb-573">是表的主键的一部分的**EntityType**表示。</span><span class="sxs-lookup"><span data-stu-id="508bb-573">Be part of the primary key of the table that the **EntityType** represents.</span></span> <span data-ttu-id="508bb-574">一个或多个**PropertyRef**元素可用于定义主键。</span><span class="sxs-lookup"><span data-stu-id="508bb-574">One or more **PropertyRef** elements can be used to define a primary key.</span></span> <span data-ttu-id="508bb-575">有关详细信息，请参阅密钥元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-575">For more information, see Key element.</span></span>
-   <span data-ttu-id="508bb-576">是引用约束的依赖端或主体端。</span><span class="sxs-lookup"><span data-stu-id="508bb-576">Be the dependent or principal end of a referential constraint.</span></span> <span data-ttu-id="508bb-577">有关详细信息，请参阅 ReferentialConstraint 元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-577">For more information, see ReferentialConstraint element.</span></span>

<span data-ttu-id="508bb-578">**PropertyRef**元素只能具有以下子元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-578">The **PropertyRef** element can only have the following child elements:</span></span>

-   <span data-ttu-id="508bb-579">文档 （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-579">Documentation (zero or one)</span></span>
-   <span data-ttu-id="508bb-580">批注元素</span><span class="sxs-lookup"><span data-stu-id="508bb-580">Annotation elements</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-581">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-581">Applicable Attributes</span></span>

<span data-ttu-id="508bb-582">下表描述了可应用于的特性**PropertyRef**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-582">The table below describes the attributes that can be applied to the **PropertyRef** element.</span></span>

| <span data-ttu-id="508bb-583">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-583">Attribute Name</span></span> | <span data-ttu-id="508bb-584">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-584">Is Required</span></span> | <span data-ttu-id="508bb-585">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-585">Value</span></span>                                |
|:---------------|:------------|:-------------------------------------|
| <span data-ttu-id="508bb-586">**名称**</span><span class="sxs-lookup"><span data-stu-id="508bb-586">**Name**</span></span>       | <span data-ttu-id="508bb-587">是</span><span class="sxs-lookup"><span data-stu-id="508bb-587">Yes</span></span>         | <span data-ttu-id="508bb-588">所引用属性的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-588">The name of the referenced property.</span></span> |

> [!NOTE]
> <span data-ttu-id="508bb-589">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**PropertyRef**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-589">Any number of annotation attributes (custom XML attributes) may be applied to the **PropertyRef** element.</span></span> <span data-ttu-id="508bb-590">然而，自定义特性可能不属于为 CSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-590">However, custom attributes may not belong to any XML namespace that is reserved for CSDL.</span></span> <span data-ttu-id="508bb-591">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-591">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-592">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-592">Example</span></span>

<span data-ttu-id="508bb-593">下面的示例演示**PropertyRef**用来通过引用定义的属性定义为主键的元素**EntityType**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-593">The following example shows a **PropertyRef** element used to define a primary key by referencing a property that is defined on an **EntityType** element.</span></span>

``` xml
 <EntityType Name="Customers">
   <Documentation>
     <Summary>Summary here.</Summary>
     <LongDescription>Long description here.</LongDescription>
   </Documentation>
   <Key>
     <PropertyRef Name="CustomerId" />
   </Key>
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
 </EntityType>
```

## <a name="referentialconstraint-element-ssdl"></a><span data-ttu-id="508bb-594">ReferentialConstraint 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-594">ReferentialConstraint Element (SSDL)</span></span>

<span data-ttu-id="508bb-595">**ReferentialConstraint**存储架构定义语言 (SSDL) 中的元素表示基础数据库中的外键约束 （也称为引用完整性约束）。</span><span class="sxs-lookup"><span data-stu-id="508bb-595">The **ReferentialConstraint** element in store schema definition language (SSDL) represents a foreign key constraint (also called a referential integrity constraint) in the underlying database.</span></span> <span data-ttu-id="508bb-596">分别由主体和依赖于子元素，指定的主体端和依赖端约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-596">The principal and dependent ends of the constraint are specified by the Principal and Dependent child elements, respectively.</span></span> <span data-ttu-id="508bb-597">PropertyRef 元素引用参与主体端和依赖端的列。</span><span class="sxs-lookup"><span data-stu-id="508bb-597">Columns that participate in the principal and dependent ends are referenced with PropertyRef elements.</span></span>

<span data-ttu-id="508bb-598">**ReferentialConstraint**元素是 Association 元素的可选子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-598">The **ReferentialConstraint** element is an optional child element of the Association element.</span></span> <span data-ttu-id="508bb-599">如果**ReferentialConstraint**元素不用于映射中指定的外键约束**关联**元素，AssociationSetMapping 元素必须用来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="508bb-599">If a **ReferentialConstraint** element is not used to map the foreign key constraint that is specified in the **Association** element, an AssociationSetMapping element must be used to do this.</span></span>

<span data-ttu-id="508bb-600">**ReferentialConstraint**元素可以具有以下子元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-600">The **ReferentialConstraint** element can have the following child elements:</span></span>

-   <span data-ttu-id="508bb-601">文档 （零个或一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-601">Documentation (zero or one)</span></span>
-   <span data-ttu-id="508bb-602">主体 （恰好一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-602">Principal (exactly one)</span></span>
-   <span data-ttu-id="508bb-603">依赖于 （恰好一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-603">Dependent (exactly one)</span></span>
-   <span data-ttu-id="508bb-604">批注元素 （零个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-604">Annotation elements (zero or more)</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-605">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-605">Applicable Attributes</span></span>

<span data-ttu-id="508bb-606">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**ReferentialConstraint**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-606">Any number of annotation attributes (custom XML attributes) may be applied to the **ReferentialConstraint** element.</span></span> <span data-ttu-id="508bb-607">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-607">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-608">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-608">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-609">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-609">Example</span></span>

<span data-ttu-id="508bb-610">下面的示例演示**关联**使用的元素**ReferentialConstraint**元素指定参与的列**FK\_CustomerOrders**外键约束：</span><span class="sxs-lookup"><span data-stu-id="508bb-610">The following example shows an **Association** element that uses a **ReferentialConstraint** element to specify the columns that participate in the **FK\_CustomerOrders** foreign key constraint:</span></span>

``` xml
 <Association Name="FK_CustomerOrders">
   <End Role="Customers"
        Type="ExampleModel.Store.Customers" Multiplicity="1">
     <OnDelete Action="Cascade" />
   </End>
   <End Role="Orders"
        Type="ExampleModel.Store.Orders" Multiplicity="*" />
   <ReferentialConstraint>
     <Principal Role="Customers">
       <PropertyRef Name="CustomerId" />
     </Principal>
     <Dependent Role="Orders">
       <PropertyRef Name="CustomerId" />
     </Dependent>
   </ReferentialConstraint>
 </Association>
```

## <a name="returntype-element-ssdl"></a><span data-ttu-id="508bb-611">ReturnType 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-611">ReturnType Element (SSDL)</span></span>

<span data-ttu-id="508bb-612">**ReturnType**元素中存储架构定义语言 (SSDL) 指定中定义的函数的返回类型**函数**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-612">The **ReturnType** element in store schema definition language (SSDL) specifies the return type for a function that is defined in a **Function** element.</span></span> <span data-ttu-id="508bb-613">此外可以使用指定返回类型的函数**ReturnType**属性。</span><span class="sxs-lookup"><span data-stu-id="508bb-613">A function return type can also be specified with a **ReturnType** attribute.</span></span>

<span data-ttu-id="508bb-614">使用指定函数的返回类型**类型**属性或**ReturnType**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-614">The return type of a function is specified with the **Type** attribute or the **ReturnType** element.</span></span>

<span data-ttu-id="508bb-615">**ReturnType**元素可以具有以下子元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-615">The **ReturnType** element can have the following child elements:</span></span>

- <span data-ttu-id="508bb-616">CollectionType （一个）</span><span class="sxs-lookup"><span data-stu-id="508bb-616">CollectionType (one)</span></span>  

> [!NOTE]
> <span data-ttu-id="508bb-617">可以将任意数量的 （自定义 XML 特性） 的批注特性应用于**ReturnType**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-617">Any number of annotation attributes (custom XML attributes) may be applied to the **ReturnType** element.</span></span> <span data-ttu-id="508bb-618">然而，自定义特性可能不属于为 SSDL 保留的任何 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-618">However, custom attributes may not belong to any XML namespace that is reserved for SSDL.</span></span> <span data-ttu-id="508bb-619">任何两个自定义特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-619">The fully-qualified names for any two custom attributes cannot be the same.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-620">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-620">Example</span></span>

<span data-ttu-id="508bb-621">下面的示例使用**函数**返回的行集合。</span><span class="sxs-lookup"><span data-stu-id="508bb-621">The following example uses a **Function** that returns a collection of rows.</span></span>

``` xml
   <Function Name="GetProducts" IsComposable="true" Schema="dbo">
     <ReturnType>
       <CollectionType>
         <RowType>
           <Property Name="ProductID" Type="int" Nullable="false" />
           <Property Name="CategoryID" Type="bigint" Nullable="false" />
           <Property Name="ProductName" Type="nvarchar" MaxLength="40" Nullable="false" />
           <Property Name="UnitPrice" Type="money" />
           <Property Name="Discontinued" Type="bit" />
         </RowType>
       </CollectionType>
     </ReturnType>
   </Function>
```


## <a name="rowtype-element-ssdl"></a><span data-ttu-id="508bb-622">RowType 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-622">RowType Element (SSDL)</span></span>

<span data-ttu-id="508bb-623">一个**RowType**元素中的以存储架构定义语言 (SSDL) 定义为返回一个未命名的结构在存储中定义的函数的类型。</span><span class="sxs-lookup"><span data-stu-id="508bb-623">A **RowType** element in store schema definition language (SSDL) defines an unnamed structure as a return type for a function defined in the store.</span></span>

<span data-ttu-id="508bb-624">一个**RowType**元素是子元素**CollectionType**元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-624">A **RowType** element is the child element of **CollectionType** element:</span></span>

<span data-ttu-id="508bb-625">一个**RowType**元素可以具有以下子元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-625">A **RowType** element can have the following child elements:</span></span>

- <span data-ttu-id="508bb-626">属性 （一个或多个）</span><span class="sxs-lookup"><span data-stu-id="508bb-626">Property (one or more)</span></span>  

### <a name="example"></a><span data-ttu-id="508bb-627">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-627">Example</span></span>

<span data-ttu-id="508bb-628">下面的示例演示使用的存储函数**CollectionType**元素来指定该函数返回的行集合 (中指定的那样**RowType**元素)。</span><span class="sxs-lookup"><span data-stu-id="508bb-628">The following example shows a store function that uses a **CollectionType** element to specify that the function returns a collection of rows (as specified in the **RowType** element).</span></span>


``` xml
   <Function Name="GetProducts" IsComposable="true" Schema="dbo">
     <ReturnType>
       <CollectionType>
         <RowType>
           <Property Name="ProductID" Type="int" Nullable="false" />
           <Property Name="CategoryID" Type="bigint" Nullable="false" />
           <Property Name="ProductName" Type="nvarchar" MaxLength="40" Nullable="false" />
           <Property Name="UnitPrice" Type="money" />
           <Property Name="Discontinued" Type="bit" />
         </RowType>
       </CollectionType>
     </ReturnType>
   </Function>
```

## <a name="schema-element-ssdl"></a><span data-ttu-id="508bb-629">Schema 元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-629">Schema Element (SSDL)</span></span>

<span data-ttu-id="508bb-630">**架构**存储架构定义语言 (SSDL) 中的元素是存储模型定义的根元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-630">The **Schema** element in store schema definition language (SSDL) is the root element of a storage model definition.</span></span> <span data-ttu-id="508bb-631">它包括构成存储模型的对象、函数和容器的定义。</span><span class="sxs-lookup"><span data-stu-id="508bb-631">It contains definitions for the objects, functions, and containers that make up a storage model.</span></span>

<span data-ttu-id="508bb-632">**架构**元素可能包含零个或多个下列子元素：</span><span class="sxs-lookup"><span data-stu-id="508bb-632">The **Schema** element may contain zero or more of the following child elements:</span></span>

-   <span data-ttu-id="508bb-633">关联</span><span class="sxs-lookup"><span data-stu-id="508bb-633">Association</span></span>
-   <span data-ttu-id="508bb-634">EntityType</span><span class="sxs-lookup"><span data-stu-id="508bb-634">EntityType</span></span>
-   <span data-ttu-id="508bb-635">EntityContainer</span><span class="sxs-lookup"><span data-stu-id="508bb-635">EntityContainer</span></span>
-   <span data-ttu-id="508bb-636">函数</span><span class="sxs-lookup"><span data-stu-id="508bb-636">Function</span></span>

<span data-ttu-id="508bb-637">**架构**元素使用**Namespace**属性来定义存储模型中的实体类型和关联对象的命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-637">The **Schema** element uses the **Namespace** attribute to define the namespace for the entity type and association objects in a storage model.</span></span> <span data-ttu-id="508bb-638">在命名空间内，任何两个对象都不能同名。</span><span class="sxs-lookup"><span data-stu-id="508bb-638">Within a namespace, no two objects can have the same name.</span></span>

<span data-ttu-id="508bb-639">存储模型命名空间是不同的 XML 命名空间**架构**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-639">A storage model namespace is different from the XML namespace of the **Schema** element.</span></span> <span data-ttu-id="508bb-640">存储模型命名空间 (由定义**Namespace**属性) 是实体类型和关联类型的逻辑容器。</span><span class="sxs-lookup"><span data-stu-id="508bb-640">A storage model namespace (as defined by the **Namespace** attribute) is a logical container for entity types and association types.</span></span> <span data-ttu-id="508bb-641">XML 命名空间 (由**xmlns**属性) 的**架构**元素是子元素和属性的默认命名空间**架构**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-641">The XML namespace (indicated by the **xmlns** attribute) of a **Schema** element is the default namespace for child elements and attributes of the **Schema** element.</span></span> <span data-ttu-id="508bb-642">窗体的 XML 命名空间http://schemas.microsoft.com/ado/YYYY/MM/edm/ssdl（其中 YYYY 和 MM 表示年和月分别） 是为 SSDL 保留。</span><span class="sxs-lookup"><span data-stu-id="508bb-642">XML namespaces of the form http://schemas.microsoft.com/ado/YYYY/MM/edm/ssdl (where YYYY and MM represent a year and month respectively) are reserved for SSDL.</span></span> <span data-ttu-id="508bb-643">自定义元素和特性不能位于具有此格式的命名空间中。</span><span class="sxs-lookup"><span data-stu-id="508bb-643">Custom elements and attributes cannot be in namespaces that have this form.</span></span>

### <a name="applicable-attributes"></a><span data-ttu-id="508bb-644">适用的特性</span><span class="sxs-lookup"><span data-stu-id="508bb-644">Applicable Attributes</span></span>

<span data-ttu-id="508bb-645">下表描述了特性可应用于**架构**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-645">The table below describes the attributes can be applied to the **Schema** element.</span></span>

| <span data-ttu-id="508bb-646">特性名</span><span class="sxs-lookup"><span data-stu-id="508bb-646">Attribute Name</span></span>            | <span data-ttu-id="508bb-647">是否必需</span><span class="sxs-lookup"><span data-stu-id="508bb-647">Is Required</span></span> | <span data-ttu-id="508bb-648">“值”</span><span class="sxs-lookup"><span data-stu-id="508bb-648">Value</span></span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|:--------------------------|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-649">**命名空间**</span><span class="sxs-lookup"><span data-stu-id="508bb-649">**Namespace**</span></span>             | <span data-ttu-id="508bb-650">是</span><span class="sxs-lookup"><span data-stu-id="508bb-650">Yes</span></span>         | <span data-ttu-id="508bb-651">存储模型的命名空间。</span><span class="sxs-lookup"><span data-stu-id="508bb-651">The namespace of the storage model.</span></span> <span data-ttu-id="508bb-652">值**Namespace**特性用于形成一种类型的完全限定的名称。</span><span class="sxs-lookup"><span data-stu-id="508bb-652">The value of the **Namespace** attribute is used to form the fully qualified name of a type.</span></span> <span data-ttu-id="508bb-653">例如，如果**EntityType**名为*客户*位于 ExampleModel.Store 命名空间，则完全限定的名称**EntityType**是ExampleModel.Store.Customer。</span><span class="sxs-lookup"><span data-stu-id="508bb-653">For example, if an **EntityType** named *Customer* is in the ExampleModel.Store namespace, then the fully qualified name of the **EntityType** is ExampleModel.Store.Customer.</span></span> <br/> <span data-ttu-id="508bb-654">以下字符串不能使用的值作为**Namespace**属性：**系统**，**暂时性**，或者**Edm**。</span><span class="sxs-lookup"><span data-stu-id="508bb-654">The following strings cannot be used as the value for the **Namespace** attribute: **System**, **Transient**, or **Edm**.</span></span> <span data-ttu-id="508bb-655">值**Namespace**属性不能与的值相同**Namespace** CSDL 架构元素中的属性。</span><span class="sxs-lookup"><span data-stu-id="508bb-655">The value for the **Namespace** attribute cannot be the same as the value for the **Namespace** attribute in the CSDL Schema element.</span></span> |
| <span data-ttu-id="508bb-656">**Alias**</span><span class="sxs-lookup"><span data-stu-id="508bb-656">**Alias**</span></span>                 | <span data-ttu-id="508bb-657">否</span><span class="sxs-lookup"><span data-stu-id="508bb-657">No</span></span>          | <span data-ttu-id="508bb-658">用于取代命名空间名称的标识符。</span><span class="sxs-lookup"><span data-stu-id="508bb-658">An identifier used in place of the namespace name.</span></span> <span data-ttu-id="508bb-659">例如，如果**EntityType**名为*客户*位于 ExampleModel.Store 命名空间和值**别名**特性是*StorageModel*，则您可以将 StorageModel.Customer 用作完全限定的名称**EntityType。**</span><span class="sxs-lookup"><span data-stu-id="508bb-659">For example, if an **EntityType** named *Customer* is in the ExampleModel.Store namespace and the value of the **Alias** attribute is *StorageModel*, then you can use StorageModel.Customer as the fully qualified name of the **EntityType.**</span></span>                                                                                                                                                                                                                                                                                    |
| <span data-ttu-id="508bb-660">**提供程序**</span><span class="sxs-lookup"><span data-stu-id="508bb-660">**Provider**</span></span>              | <span data-ttu-id="508bb-661">是</span><span class="sxs-lookup"><span data-stu-id="508bb-661">Yes</span></span>         | <span data-ttu-id="508bb-662">数据提供程序。</span><span class="sxs-lookup"><span data-stu-id="508bb-662">The data provider.</span></span>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| <span data-ttu-id="508bb-663">**ProviderManifestToken**</span><span class="sxs-lookup"><span data-stu-id="508bb-663">**ProviderManifestToken**</span></span> | <span data-ttu-id="508bb-664">是</span><span class="sxs-lookup"><span data-stu-id="508bb-664">Yes</span></span>         | <span data-ttu-id="508bb-665">一个标记，该标记指示提供程序清单返回到的提供程序。</span><span class="sxs-lookup"><span data-stu-id="508bb-665">A token that indicates to the provider which provider manifest to return.</span></span> <span data-ttu-id="508bb-666">没有为该标记定义格式。</span><span class="sxs-lookup"><span data-stu-id="508bb-666">No format for the token is defined.</span></span> <span data-ttu-id="508bb-667">标记的值由提供程序定义。</span><span class="sxs-lookup"><span data-stu-id="508bb-667">Values for the token are defined by the provider.</span></span> <span data-ttu-id="508bb-668">有关 SQL Server 提供程序清单标记信息，请参阅实体框架的 SqlClient。</span><span class="sxs-lookup"><span data-stu-id="508bb-668">For information about SQL Server provider manifest tokens, see SqlClient for Entity Framework.</span></span>                                                                                                                                                                                                                                                                                                                        |

### <a name="example"></a><span data-ttu-id="508bb-669">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-669">Example</span></span>

<span data-ttu-id="508bb-670">下面的示例演示**架构**元素，其中包含**EntityContainer**元素、 两个**EntityType**元素，其中一个**关联**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-670">The following example shows a **Schema** element that contains an **EntityContainer** element, two **EntityType** elements, and one **Association** element.</span></span>

``` xml
 <Schema Namespace="ExampleModel.Store"
       Alias="Self" Provider="System.Data.SqlClient"
       ProviderManifestToken="2008"
       xmlns="http://schemas.microsoft.com/ado/2009/11/edm/ssdl">
   <EntityContainer Name="ExampleModelStoreContainer">
     <EntitySet Name="Customers"
                EntityType="ExampleModel.Store.Customers"
                Schema="dbo" />
     <EntitySet Name="Orders"
                EntityType="ExampleModel.Store.Orders"
                Schema="dbo" />
     <AssociationSet Name="FK_CustomerOrders"
                     Association="ExampleModel.Store.FK_CustomerOrders">
       <End Role="Customers" EntitySet="Customers" />
       <End Role="Orders" EntitySet="Orders" />
     </AssociationSet>
   </EntityContainer>
   <EntityType Name="Customers">
     <Documentation>
       <Summary>Summary here.</Summary>
       <LongDescription>Long description here.</LongDescription>
     </Documentation>
     <Key>
       <PropertyRef Name="CustomerId" />
     </Key>
     <Property Name="CustomerId" Type="int" Nullable="false" />
     <Property Name="Name" Type="nvarchar(max)" Nullable="false" />
   </EntityType>
   <EntityType Name="Orders" xmlns:c="http://CustomNamespace">
     <Key>
       <PropertyRef Name="OrderId" />
     </Key>
     <Property Name="OrderId" Type="int" Nullable="false"
               c:CustomAttribute="someValue"/>
     <Property Name="ProductId" Type="int" Nullable="false" />
     <Property Name="Quantity" Type="int" Nullable="false" />
     <Property Name="CustomerId" Type="int" Nullable="false" />
     <c:CustomElement>
       Custom data here.
     </c:CustomElement>
   </EntityType>
   <Association Name="FK_CustomerOrders">
     <End Role="Customers"
          Type="ExampleModel.Store.Customers" Multiplicity="1">
       <OnDelete Action="Cascade" />
     </End>
     <End Role="Orders"
          Type="ExampleModel.Store.Orders" Multiplicity="*" />
     <ReferentialConstraint>
       <Principal Role="Customers">
         <PropertyRef Name="CustomerId" />
       </Principal>
       <Dependent Role="Orders">
         <PropertyRef Name="CustomerId" />
       </Dependent>
     </ReferentialConstraint>
   </Association>
   <Function Name="UpdateOrderQuantity"
             Aggregate="false"
             BuiltIn="false"
             NiladicFunction="false"
             IsComposable="false"
             ParameterTypeSemantics="AllowImplicitConversion"
             Schema="dbo">
     <Parameter Name="orderId" Type="int" Mode="In" />
     <Parameter Name="newQuantity" Type="int" Mode="In" />
   </Function>
   <Function Name="UpdateProductInOrder" IsComposable="false">
     <CommandText>
       UPDATE Orders
       SET ProductId = @productId
       WHERE OrderId = @orderId;
     </CommandText>
     <Parameter Name="productId"
                Mode="In"
                Type="int"/>
     <Parameter Name="orderId"
                Mode="In"
                Type="int"/>
   </Function>
 </Schema>
```

## <a name="annotation-attributes"></a><span data-ttu-id="508bb-671">Annotation 特性</span><span class="sxs-lookup"><span data-stu-id="508bb-671">Annotation Attributes</span></span>

<span data-ttu-id="508bb-672">以存储架构定义语言 (SSDL) 表示的批注特性在存储模型中是自定义 XML 特性，这些特性提供有关存储模型中元素的额外元数据。</span><span class="sxs-lookup"><span data-stu-id="508bb-672">Annotation attributes in store schema definition language (SSDL) are custom XML attributes in the storage model that provide extra metadata about the elements in the storage model.</span></span> <span data-ttu-id="508bb-673">除了具有有效的 XML 结构之外，以下约束也适用于批注特性：</span><span class="sxs-lookup"><span data-stu-id="508bb-673">In addition to having valid XML structure, the following constraints apply to annotation attributes:</span></span>

-   <span data-ttu-id="508bb-674">批注特性不能位于为 SSDL 保留的任何 XML 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="508bb-674">Annotation attributes must not be in any XML namespace that is reserved for SSDL.</span></span>
-   <span data-ttu-id="508bb-675">任何两个批注特性的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-675">The fully-qualified names of any two annotation attributes must not be the same.</span></span>

<span data-ttu-id="508bb-676">可以将多个批注特性应用于一个给定的 SSDL 元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-676">More than one annotation attribute may be applied to a given SSDL element.</span></span> <span data-ttu-id="508bb-677">可以使用 System.Data.Metadata.Edm 命名空间中的类，在运行时访问批注元素中包含的元数据。</span><span class="sxs-lookup"><span data-stu-id="508bb-677">Metadata contained in annotation elements can be accessed at runtime by using classes in the System.Data.Metadata.Edm namespace.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-678">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-678">Example</span></span>

<span data-ttu-id="508bb-679">下面的示例演示一个具有将批注特性应用到的 EntityType 元素**OrderId**属性。</span><span class="sxs-lookup"><span data-stu-id="508bb-679">The following example shows an EntityType element that has an annotation attribute applied to the **OrderId** property.</span></span> <span data-ttu-id="508bb-680">本示例还演示批注元素添加到**EntityType**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-680">The example also show an annotation element added to the **EntityType** element.</span></span>

``` xml
 <EntityType Name="Orders" xmlns:c="http://CustomNamespace">
   <Key>
     <PropertyRef Name="OrderId" />
   </Key>
   <Property Name="OrderId" Type="int" Nullable="false"
             c:CustomAttribute="someValue"/>
   <Property Name="ProductId" Type="int" Nullable="false" />
   <Property Name="Quantity" Type="int" Nullable="false" />
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <c:CustomElement>
     Custom data here.
   </c:CustomElement>
 </EntityType>
```

## <a name="annotation-elements-ssdl"></a><span data-ttu-id="508bb-681">批注元素 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-681">Annotation Elements (SSDL)</span></span>

<span data-ttu-id="508bb-682">以存储架构定义语言 (SSDL) 表示的批注元素是存储模型中的自定义 XML 元素，可提供有关存储模型的额外元数据。</span><span class="sxs-lookup"><span data-stu-id="508bb-682">Annotation elements in store schema definition language (SSDL) are custom XML elements in the storage model that provide extra metadata about the storage model.</span></span> <span data-ttu-id="508bb-683">除了具有有效的 XML 结构之外，批注元素还应满足以下约束：</span><span class="sxs-lookup"><span data-stu-id="508bb-683">In addition to having valid XML structure, the following constraints apply to annotation elements:</span></span>

-   <span data-ttu-id="508bb-684">批注元素不能位于为 SSDL 保留的任何 XML 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="508bb-684">Annotation elements must not be in any XML namespace that is reserved for SSDL.</span></span>
-   <span data-ttu-id="508bb-685">任何两个批注元素的完全限定名称都不能相同。</span><span class="sxs-lookup"><span data-stu-id="508bb-685">The fully-qualified names of any two annotation elements must not be the same.</span></span>
-   <span data-ttu-id="508bb-686">批注元素必须出现在给定 SSDL 元素的所有其他子元素之后。</span><span class="sxs-lookup"><span data-stu-id="508bb-686">Annotation elements must appear after all other child elements of a given SSDL element.</span></span>

<span data-ttu-id="508bb-687">多个批注元素可能是某个给定 SSDL 元素的子元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-687">More than one annotation element may be a child of a given SSDL element.</span></span> <span data-ttu-id="508bb-688">从.NET Framework 版本 4 开始，访问元数据批注元素中包含可以在运行时使用 System.Data.Metadata.Edm 命名空间中的类。</span><span class="sxs-lookup"><span data-stu-id="508bb-688">Starting with the .NET Framework version 4, metadata contained in annotation elements can be accessed at runtime by using classes in the System.Data.Metadata.Edm namespace.</span></span>

### <a name="example"></a><span data-ttu-id="508bb-689">示例</span><span class="sxs-lookup"><span data-stu-id="508bb-689">Example</span></span>

<span data-ttu-id="508bb-690">下面的示例演示一个具有一个批注元素的 EntityType 元素 (**CustomElement**)。</span><span class="sxs-lookup"><span data-stu-id="508bb-690">The following example shows an EntityType element that has an annotation element (**CustomElement**).</span></span> <span data-ttu-id="508bb-691">该示例还显示应用于的批注特性**OrderId**属性。</span><span class="sxs-lookup"><span data-stu-id="508bb-691">The example also shows an annotation attribute applied to the **OrderId** property.</span></span>

``` xml
 <EntityType Name="Orders" xmlns:c="http://CustomNamespace">
   <Key>
     <PropertyRef Name="OrderId" />
   </Key>
   <Property Name="OrderId" Type="int" Nullable="false"
             c:CustomAttribute="someValue"/>
   <Property Name="ProductId" Type="int" Nullable="false" />
   <Property Name="Quantity" Type="int" Nullable="false" />
   <Property Name="CustomerId" Type="int" Nullable="false" />
   <c:CustomElement>
     Custom data here.
   </c:CustomElement>
 </EntityType>
```

## <a name="facets-ssdl"></a><span data-ttu-id="508bb-692">方面 (SSDL)</span><span class="sxs-lookup"><span data-stu-id="508bb-692">Facets (SSDL)</span></span>

<span data-ttu-id="508bb-693">方面以存储架构定义语言 (SSDL) 表示的属性元素中指定的列类型的约束。</span><span class="sxs-lookup"><span data-stu-id="508bb-693">Facets in store schema definition language (SSDL) represent constraints on column types that are specified in Property elements.</span></span> <span data-ttu-id="508bb-694">方面作为 XML 特性实现上**属性**元素。</span><span class="sxs-lookup"><span data-stu-id="508bb-694">Facets are implemented as XML attributes on **Property** elements.</span></span>

<span data-ttu-id="508bb-695">下表描述了 SSDL 中支持的方面：</span><span class="sxs-lookup"><span data-stu-id="508bb-695">The following table describes the facets that are supported in SSDL:</span></span>

| <span data-ttu-id="508bb-696">方面</span><span class="sxs-lookup"><span data-stu-id="508bb-696">Facet</span></span>           | <span data-ttu-id="508bb-697">描述</span><span class="sxs-lookup"><span data-stu-id="508bb-697">Description</span></span>                                                                                                                                                                                                                                                 |
|:----------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="508bb-698">**排序规则**</span><span class="sxs-lookup"><span data-stu-id="508bb-698">**Collation**</span></span>   | <span data-ttu-id="508bb-699">指定在对属性值执行比较和排序操作时要使用的排序序列。</span><span class="sxs-lookup"><span data-stu-id="508bb-699">Specifies the collating sequence (or sorting sequence) to be used when performing comparison and ordering operations on values of the property.</span></span>                                                                                                             |
| <span data-ttu-id="508bb-700">**FixedLength**</span><span class="sxs-lookup"><span data-stu-id="508bb-700">**FixedLength**</span></span> | <span data-ttu-id="508bb-701">指定列值的长度是否可变。</span><span class="sxs-lookup"><span data-stu-id="508bb-701">Specifies whether the length of the column value can vary.</span></span>                                                                                                                                                                                                  |
| <span data-ttu-id="508bb-702">**MaxLength**</span><span class="sxs-lookup"><span data-stu-id="508bb-702">**MaxLength**</span></span>   | <span data-ttu-id="508bb-703">指定列值的最大长度。</span><span class="sxs-lookup"><span data-stu-id="508bb-703">Specifies the maximum length of the column value.</span></span>                                                                                                                                                                                                           |
| <span data-ttu-id="508bb-704">**精度**</span><span class="sxs-lookup"><span data-stu-id="508bb-704">**Precision**</span></span>   | <span data-ttu-id="508bb-705">类型的属性**十进制**，指定属性值可以具有的位数。</span><span class="sxs-lookup"><span data-stu-id="508bb-705">For properties of type **Decimal**, specifies the number of digits a property value can have.</span></span> <span data-ttu-id="508bb-706">类型的属性**时间**， **DateTime**，并**DateTimeOffset**，指定列值的秒的小数部分的位数。</span><span class="sxs-lookup"><span data-stu-id="508bb-706">For properties of type **Time**, **DateTime**, and **DateTimeOffset**, specifies the number of digits for the fractional part of seconds of the column value.</span></span> |
| <span data-ttu-id="508bb-707">缩放</span><span class="sxs-lookup"><span data-stu-id="508bb-707">**Scale**</span></span>       | <span data-ttu-id="508bb-708">指定列值小数点右侧的位数。</span><span class="sxs-lookup"><span data-stu-id="508bb-708">Specifies the number of digits to the right of the decimal point for the column value.</span></span>                                                                                                                                                                      |
| <span data-ttu-id="508bb-709">**Unicode**</span><span class="sxs-lookup"><span data-stu-id="508bb-709">**Unicode**</span></span>     | <span data-ttu-id="508bb-710">指示是否将列值存储为 Unicode。</span><span class="sxs-lookup"><span data-stu-id="508bb-710">Indicates whether the column value is stored as Unicode.</span></span>                                                                                                                                                                                                    |