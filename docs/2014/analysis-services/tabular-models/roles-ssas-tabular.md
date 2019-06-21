---
title: Roles (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd4e54a0099e459d52577de23acc5c4f2989edc5
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284859"
---
# <a name="roles-ssas-tabular"></a>Roles (SSAS tabular)
  Los roles, en los modelos tabulares, definen los permisos de los miembros para un modelo. Cada rol contiene miembros, por nombre de usuario de Windows o por grupo de Windows, y permisos (de lectura, de procesamiento, de administrador). Los miembros del rol pueden realizar en el modelo las acciones definidas por el permiso de rol. Los roles que se han definido con permisos de lectura también pueden proporcionar seguridad adicional en el nivel de fila mediante filtros de fila.  
  
> [!IMPORTANT]  
>  Para que los usuarios se puedan conectar a un modelo implementado mediante una aplicación cliente de informes o de análisis de datos, debe crear al menos un rol del que sean miembros esos usuarios que tenga al menos permiso de lectura.  
  
 La información de este tema va dirigida a los autores de modelos tabulares que definen los roles mediante el cuadro de diálogo Administrador de roles de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Los roles definidos durante la creación del modelo se aplican a la base de datos del área de trabajo del modelo. Después de implementar una base de datos modelo, los administradores de la base de datos modelo podrán administrar (agregar, modificar, eliminar) los miembros de roles con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener información sobre cómo administrar miembros de roles en una base de datos implementada, vea [Roles de modelos tabulares &#40;SSAS tabular&#41;](tabular-model-roles-ssas-tabular.md).  
  
 En [Creación de modelos tabulares &#40;tutorial de Adventure Works&#41;](../tabular-modeling-adventure-works-tutorial.md) encontrará información adicional y lecciones sobre cómo usar esta característica.  
  
 Secciones de este tema:  
  
-   [Descripción de los roles](#bkmk_underst)  
  
-   [Permissions](#bkmk_permissions)  
  
-   [Filtros de fila](#bkmk_rowfliters)  
  
-   [Prueba de roles](#bkmk_testroles)  
  
-   [Tareas relacionadas](#bkmk_rt)  
  
##  <a name="bkmk_underst"></a> Descripción de los roles  
 Los roles se usan en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para administrar la seguridad de los objetos y los datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Hay dos tipos de roles en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   El rol del servidor, que es un rol fijo que proporciona acceso de administrador a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Los roles de base de datos, que son roles definidos por los autores del modelo para controlar el acceso de los usuarios que no son administradores a una base de datos de modelo y a los datos.  
  
 Los roles definidos para un modelo tabular son roles de base de datos. Es decir, los roles contienen miembros que son usuarios o grupos de Windows con permisos específicos que definen las acciones que pueden realizar en la base de datos del modelo. Un rol de base de datos se crea como objeto independiente en la base de datos y solo se aplica a la base de datos en la que se crea el rol. El autor del modelo que, de forma predeterminada, tiene permisos de administrador en el servidor de bases de datos del área de trabajo, incluye a los usuarios y/o grupos de Windows en el rol; para un modelo implementado, lo hace un administrador.  
  
 Use los filtros de fila para definir de forma más exhaustiva los roles en los modelos tabulares. Los filtros de fila usan expresiones DAX para definir las filas de una tabla, así como las filas relacionadas en las distintas direcciones, que los usuarios pueden consultar. Los filtros de fila que usen expresiones de DAX solo se pueden definir para los permisos de lectura y de lectura y procesamiento. Para obtener más información, vea [Row Filters](#bkmk_rowfliters) , más adelante en este tema.  
  
 De forma predeterminada, cuando se crea un proyecto de modelos tabulares, el proyecto no tiene ningún rol. Los roles se pueden definir mediante el cuadro de diálogo Administrador de roles de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Si los roles se definen durante la creación del modelo, se aplican a la base de datos del área de trabajo del modelo. Cuando se implementa el modelo, se le aplican los mismos roles. Una vez implementado el modelo, los miembros del rol de servidor (administrador de[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ) y los administradores de bases de datos pueden administrar los roles asociados al modelo y los miembros asociados con cada rol mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  Los roles definidos para un modelo configurado para el modo DirectQuery no pueden usar filtros de fila; sin embargo, se aplicarán los permisos definidos para cada rol.  
  
##  <a name="bkmk_permissions"></a> Permisos  
 Cada rol tiene un único permiso de base de datos definido (excepto en el caso del permiso de lectura y procesamiento combinado). De forma predeterminada, los roles tienen el permiso Ninguno. Es decir, una vez que se agreguen los miembros al rol con el permiso Ninguno, estos no podrán modificar la base de datos, ejecutar una operación de proceso, consultar los datos ni ver la base de datos a menos que se conceda un permiso diferente.  
  
 Un grupo o usuario de Windows puede ser miembro de varios roles, cada uno de ellos con un permiso distinto. Cuando un usuario es miembro de varios roles, los permisos definidos para cada uno de ellos son acumulativos. Por ejemplo, si un usuario es miembro de un rol que tiene el permiso de lectura y de otro que tiene el permiso Ninguno, dicho usuario tendrá permisos de lectura.  
  
 Cada rol puede tener uno de los permisos siguientes definidos:  
  
|Permisos|Descripción|Filtros de filas con DAX|  
|-----------------|-----------------|----------------------------|  
|None|Los miembros no pueden realizar ninguna modificación en el esquema de la base de datos modelo y no pueden consultar los datos.|No se pueden aplicar filtros de fila. No hay datos visibles para los usuarios de este rol|  
|Lectura|Los miembros pueden consultar los datos (según los filtros de fila) pero no pueden ver la base de datos modelo en SSMS, no pueden realizar cambios en el esquema de la base de datos modelo y el usuario no puede procesar el modelo.|Se pueden aplicar filtros de fila. Solamente están visibles para los usuarios los datos especificados en la fórmula DAX del filtro de fila.|  
|Leer y actualizar|Los miembros pueden consultar los datos (según los filtros de fila) y ejecutar operaciones de proceso mediante la ejecución de un script o un paquete que contenga un comando de proceso, pero no pueden realizar ningún cambio en la base de datos. No pueden ver la base de datos del modelo en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|Se pueden aplicar filtros de fila. Solo se pueden consultar los datos especificados en la fórmula DAX del filtro de filas.|  
|Procesar|Los miembros pueden ejecutar operaciones de proceso mediante la ejecución de un script o un paquete que contenga un comando de proceso. No se puede modificar el esquema de la base de datos de modelo. No se pueden consultar los datos. No puede consultar la base de datos del modelo en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|No se pueden aplicar filtros de fila. No se pueden consultar datos en este rol|  
|Administrador|Los miembros pueden realizar modificaciones en el esquema del modelo y consultar todos los datos en el diseñador de modelos, el cliente de informes y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|No se pueden aplicar filtros de fila. Todos los datos se pueden consultar datos en este rol.|  
  
##  <a name="bkmk_rowfliters"></a> Filtros de fila  
 Los filtros de fila definen las filas de una tabla que pueden ser consultadas por un rol determinado. Los filtros de fila se definen para cada tabla de un modelo mediante fórmulas de DAX.  
  
 Los filtros de fila solo se pueden definir para los roles que tengan permisos de lectura y de lectura y procesamiento. De forma predeterminada, si no se define un filtro de fila para una tabla determinada, los miembros de un rol que tenga permisos de lectura o de lectura y procesamiento pueden consultar todas las filas de la tabla, a menos que se aplique un filtro cruzado de otra tabla.  
  
 Una vez definido un filtro de fila para una tabla determinada, una fórmula DAX, que debe devolver un valor TRUE/FALSE, será la que defina las filas que pueden ser consultadas por los miembros de ese rol en especial. Las filas no incluidas en la fórmula DAX no podrán ser consultadas. Por ejemplo, para los miembros del rol Sales, la tabla Customers con la fila de la siguiente expresión de filtro, *= Customers [Country] = "USA"* , los miembros del rol Sales, solo podrán ver clientes de Estados Unidos.  
  
 Los filtros de fila se aplican a las filas especificadas y también a las filas relacionadas. Si una tabla tiene varias relaciones, los filtros aplican seguridad a la relación que está activa. Los filtros de fila se intersecarán con otros filtros de fila definidos para las tablas relacionadas, por ejemplo:  
  
|Table|DAX expression|  
|-----------|--------------------|  
|Region|=Region[Country]="USA"|  
|ProductCategory|=ProductCategory[Name]="Bicycles"|  
|Transactions|=Transactions[Year]=2008|  
  
 El efecto neto de estos permisos en la tabla Transactions es que los miembros podrán consultar las filas de datos en las que el cliente sea de los EE. UU., la categoría de producto sea bicycles y el año sea 2008. Los usuarios no podrán consultar ninguna de las transacciones que no cumplan las tres condiciones anteriores, a menos que sean miembros de otro rol que les conceda estos permisos.  
  
 Puede usar el filtro *=FALSE()* para denegar el acceso a todas las filas de una tabla completa.  
  
### <a name="dynamic-security"></a>Seguridad dinámica  
 Seguridad dinámica proporciona una manera de definir la seguridad en el nivel de fila según el nombre del usuario que ha iniciado sesión actualmente o la propiedad CustomData devuelta por una cadena de conexión. Para implementar seguridad dinámica, debe incluir en el modelo una tabla con los valores de inicio de sesión (nombre de usuario de Windows) para los usuarios, así como un campo que se pueda utilizar para definir un permiso específico; por ejemplo, una tabla de los dimEmployees con un Id. de acceso (dominio \ nombredeusuario) junto con un valor de departamento para cada empleado.  
  
 Para implementar seguridad dinámica, puede utilizar las siguientes funciones como parte de una fórmula DAX para devolver el nombre del usuario que ha iniciado sesión actualmente, o la propiedad CustomData en una cadena de conexión:  
  
|Función|Descripción|  
|--------------|-----------------|  
|[Función USERNAME &#40;DAX&#41;](/dax/username-function-dax)|Devuelve el dominio\nombredeusuario del usuario que ha iniciado sesión actualmente.|  
|[Función CUSTOMDATA &#40;DAX&#41;](/dax/customdata-function-dax)|Devuelve la propiedad CustomData en una cadena de conexión.|  
  
 Puede utilizar la función LOOKUPVALUE para devolver valores para una columna en la que el nombre de usuario de Windows sea el mismo que el nombre de usuario devuelto por la función USERNAME o una cadena devuelta por la función CustomData. Las consultas se pueden restringir a los casos en que los valores devueltos por LOOKUPVALUE coincidan con los valores en la misma tabla o en una tabla relacionada.  
  
 Por ejemplo, con esta fórmula:  
  
 `='dimDepartmentGroup'[DepartmentGroupId]=LOOKUPVALUE('dimEmployees'[DepartmentGroupId], 'dimEmployees'[LoginId], USERNAME(), 'dimEmployees'[LoginId], 'dimDepartmentGroup'[DepartmentGroupId])`  
  
 La función LOOKUPVALUE devuelve valores para la columna dimEmployees [DepartmentId] donde el valor de dimEmployees LoginId [] es el mismo que el LoginID del usuario que ha iniciado sesión actualmente, devuelto por USERNAME, y los valores de dimEmployees DepartmentId [] son los mismos que los de dimDepartmentGroup [DepartmentId]. Los valores de DepartmentId devueltos por LOOKUPVALUE se usan para limitar las filas consultadas en la tabla de dimDepartment, y cualquier tabla relacionada por DepartmentId. Solo se devolverán las filas donde DepartmentId esté también en los valores de DepartmentId devueltos por la función LOOKUPVALUE.  
  
 **dimEmployees**  
  
|LastName|FirstName|LoginID|DepartmentName|DepartmentId|  
|--------------|---------------|-------------|--------------------|------------------|  
|Brown|Kevin|Adventure-works\kevin0|Marketing|7|  
|Bradley|David|Adventure-works\david0|Marketing|7|  
|Dobney|JoLynn|Adventure-works\JoLynn0|Production|4|  
|Baretto DeMattos|Paula|Adventure-works\Paula0|Human Resources|2|  
  
 **dimDepartment**  
  
|DepartmentId|DepartmentName|  
|------------------|--------------------|  
|1|Corporate|  
|2|Executive General and Administration|  
|3|Inventory Management|  
|4|Manufacturing|  
|5|Quality Assurance|  
|6|Research and Development|  
|7|Sales and Marketing|  
  
##  <a name="bkmk_testroles"></a> Prueba de roles  
 Al crear un proyecto de modelos, puede usar la característica Analizar en Excel para probar la eficacia de los roles que ha definido. En el menú **Modelo** del diseñador de modelos, al hacer clic en **Analizar en Excel**, y antes de que se inicie Excel, aparecerá el cuadro de diálogo **Elegir credenciales y perspectivas** . En este cuadro de diálogo, puede especificar el nombre de usuario actual, otro nombre de usuario, un rol y una perspectiva que usará para conectar con el modelo del área de trabajo como un origen de datos. Para obtener más información, vea [Analizar en Excel &#40;SSAS tabular&#41;](analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Tareas relacionadas  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Crear y administrar roles &#40;SSAS tabular&#41;](create-and-manage-roles-ssas-tabular.md)|Las tareas de este tema explican cómo crear y administrar roles mediante el cuadro de diálogo **Administrador de roles** del diseñador de modelos.|  
  
## <a name="see-also"></a>Vea también  
 [Perspectivas &#40;SSAS tabular&#41;](perspectives-ssas-tabular.md)   
 [Analizar en Excel &#40;SSAS tabular&#41;](analyze-in-excel-ssas-tabular.md)   
 [Función USERNAME &#40;DAX&#41;](/dax/username-function-dax)   
 [La función LOOKUPVALUE &#40;DAX&#41;](/dax/lookupvalue-function-dax)   
 [Función CUSTOMDATA &#40;DAX&#41;](/dax/customdata-function-dax)  
  
  
