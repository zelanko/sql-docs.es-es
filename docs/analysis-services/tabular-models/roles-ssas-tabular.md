---
title: Roles (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: bbbcfdbaafa7e5cbc17defc91b5dc7e391d92ad6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="roles"></a>Roles
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Roles, en los modelos tabulares, definen los permisos de miembro para un modelo. Los miembros del rol pueden realizar en el modelo las acciones definidas por el permiso de rol. Los roles que se han definido con permisos de lectura también pueden proporcionar seguridad adicional en el nivel de fila mediante filtros de fila. 
  
 Para SQL Server Analysis Services, roles contienen a miembros de usuario por nombre de usuario o grupo de Windows y permisos (lectura, process, administrador). Para los servicios de análisis de Azure, los usuarios deben estar en su Azure Active Directory y los nombres de usuario y grupos especificados deben ser por una dirección de correo electrónico profesional o UPN. 
  
> [!IMPORTANT]  
>  Para que los usuarios se conecten a un modelo implementado mediante el uso de una aplicación de cliente de informes, debe crear al menos un rol con al menos el permiso para que los usuarios son miembros de lectura.  
  
 Información de este tema está destinado a los autores de modelos tabulares que definen los roles mediante el cuadro de diálogo Administrador de roles en SSDT. Los roles definidos durante la creación del modelo se aplican a la base de datos del área de trabajo del modelo. Una vez implementada una base de datos de modelo, pueden administrar los administradores de base de datos de modelo (agregar, editar y eliminar) los miembros del rol mediante SSMS. Para obtener información acerca de cómo administrar los miembros de roles en una base de datos implementada, vea [Roles de modelos tabulares](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
##  <a name="bkmk_underst"></a> Understanding roles  
 Las funciones se usan en Analysis Services para administrar el acceso de datos de modelo. Hay dos tipos de roles:  
  
-   El rol de servidor, un rol fijo que proporciona acceso de administrador a una instancia de servidor de Analysis Services.  
  
-   Los roles de base de datos, que son roles definidos por los autores del modelo para controlar el acceso de los usuarios que no son administradores a una base de datos de modelo y a los datos.  
  
 Los roles definidos para un modelo tabular son roles de base de datos. Es decir, los roles contienen a miembros que consta de los usuarios o grupos que tengan permisos específicos que definen las acciones que esos miembros pueden realizar en la base de datos de modelo. Un rol de base de datos se crea como objeto independiente en la base de datos y solo se aplica a la base de datos en la que se crea el rol. Usuarios y grupos que se incluyen en el rol por el autor del modelo, que, de forma predeterminada, tiene permisos de administrador en el servidor de base de datos del área de trabajo; para un modelo implementado por un administrador.  
  
 Use los filtros de fila para definir de forma más exhaustiva los roles en los modelos tabulares. Los filtros de fila usan expresiones DAX para definir las filas de una tabla, así como las filas relacionadas en las distintas direcciones, que los usuarios pueden consultar. Los filtros de fila que usen expresiones de DAX solo se pueden definir para los permisos de lectura y de lectura y procesamiento. Para obtener más información, consulte [filtros de fila](#bkmk_rowfliters) más adelante en este tema.  
  
 De forma predeterminada, cuando se crea un proyecto de modelos tabulares, el proyecto no tiene ningún rol. Las funciones pueden definirse mediante el cuadro de diálogo Administrador de roles en SSDT. Si los roles se definen durante la creación del modelo, se aplican a la base de datos del área de trabajo del modelo. Cuando se implementa el modelo, se le aplican los mismos roles. Después de que se ha implementado un modelo, los miembros del rol de servidor ([Administrador de Analysis Services) y los administradores de base de datos pueden administrar los roles asociados con el modelo y los miembros asociados a cada rol mediante SSMS.  
  
##  <a name="bkmk_permissions"></a> Permisos  
 Cada rol tiene un único permiso de base de datos definido (excepto en el caso del permiso de lectura y procesamiento combinado). De forma predeterminada, los roles tienen el permiso Ninguno. Es decir, una vez que se agreguen los miembros al rol con el permiso Ninguno, estos no podrán modificar la base de datos, ejecutar una operación de proceso, consultar los datos ni ver la base de datos a menos que se conceda un permiso diferente.  
  
 Un usuario o grupo puede ser un miembro de varios roles, cada rol con un permiso diferente. Cuando un usuario es miembro de varios roles, los permisos definidos para cada uno de ellos son acumulativos. Por ejemplo, si un usuario es miembro de un rol que tiene el permiso de lectura y de otro que tiene el permiso Ninguno, dicho usuario tendrá permisos de lectura.  
  
 Cada rol puede tener uno de los permisos siguientes definidos:  
  
|Permissions|Description|Filtros de filas con DAX|  
|-----------------|-----------------|----------------------------|  
|None|Los miembros no pueden realizar ninguna modificación en el esquema de la base de datos modelo y no pueden consultar los datos.|No se pueden aplicar filtros de fila. No hay datos visibles para los usuarios de este rol|  
|Lectura|Los miembros pueden consultar los datos (según los filtros de fila) pero no pueden ver la base de datos modelo en SSMS, no pueden realizar cambios en el esquema de la base de datos modelo y el usuario no puede procesar el modelo.|Se pueden aplicar filtros de fila. Solamente están visibles para los usuarios los datos especificados en la fórmula DAX del filtro de fila.|  
|Leer y actualizar|Los miembros pueden consultar los datos (según los filtros de fila) y ejecutar operaciones de proceso mediante la ejecución de un script o un paquete que contenga un comando de proceso, pero no pueden realizar ningún cambio en la base de datos. No se puede ver la base de datos de modelo en SSMS.|Se pueden aplicar filtros de fila. Solo se pueden consultar los datos especificados en la fórmula DAX del filtro de filas.|  
|Procesar|Los miembros pueden ejecutar operaciones de proceso mediante la ejecución de un script o un paquete que contenga un comando de proceso. No se puede modificar el esquema de la base de datos de modelo. No se pueden consultar los datos. No se puede consultar la base de datos de modelo en SSMS.|No se pueden aplicar filtros de fila. No se pueden consultar datos en este rol|  
|Administrador|Los miembros pueden realizar modificaciones en el esquema del modelo y pueden consultar todos los datos en el Diseñador de modelos, el cliente de informes y el SSMS.|No se pueden aplicar filtros de fila. Todos los datos se pueden consultar datos en este rol.|  
  
##  <a name="bkmk_rowfliters"></a> Row filters  
 Los filtros de fila definen las filas de una tabla que pueden ser consultadas por un rol determinado. Los filtros de fila se definen para cada tabla de un modelo mediante fórmulas de DAX.  
  
 Los filtros de fila solo se pueden definir para los roles que tengan permisos de lectura y de lectura y procesamiento. De forma predeterminada, si no se define un filtro de fila para una tabla determinada, los miembros de un rol que tenga permisos de lectura o de lectura y procesamiento pueden consultar todas las filas de la tabla, a menos que se aplique un filtro cruzado de otra tabla.  
  
 Una vez definido un filtro de fila para una tabla determinada, una fórmula DAX, que debe devolver un valor TRUE/FALSE, será la que defina las filas que pueden ser consultadas por los miembros de ese rol en especial. Las filas no incluidas en la fórmula DAX no podrán ser consultadas. Por ejemplo, en el caso de los miembros del rol Sales, si la tabla Customers tiene la expresión de filtro de fila *=Customers [Country] = “USA”*, solo los miembros de dicho rol podrán ver clientes de EE. UU.  
  
 Los filtros de fila se aplican a las filas especificadas y también a las filas relacionadas. Si una tabla tiene varias relaciones, los filtros aplican seguridad a la relación que está activa. Los filtros de fila se intersecarán con otros filtros de fila definidos para las tablas relacionadas, por ejemplo:  
  
|Table|DAX expression|  
|-----------|--------------------|  
|Region|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|Transactions|=Transactions[Year]=2008|  
  
 El efecto neto de estos permisos en la tabla Transactions es que los miembros podrán consultar las filas de datos en las que el cliente sea de los EE. UU., la categoría de producto sea bicycles y el año sea 2008. Los usuarios no podrán consultar ninguna de las transacciones que no cumplan las tres condiciones anteriores, a menos que sean miembros de otro rol que les conceda estos permisos.  
  
 Puede usar el filtro *=FALSE()*para denegar el acceso a todas las filas de una tabla completa.  
  
### <a name="dynamic-security"></a>Seguridad dinámica  
 Seguridad dinámica proporciona una manera de definir la seguridad en el nivel de fila según el nombre del usuario que ha iniciado sesión actualmente o la propiedad CustomData devuelta por una cadena de conexión. Para implementar seguridad dinámica, debe incluir en el modelo una tabla con los valores de inicio de sesión (nombre de usuario de Windows) para los usuarios, así como un campo que se pueda utilizar para definir un permiso específico; por ejemplo, una tabla de los dimEmployees con un Id. de acceso (dominio \ nombredeusuario) junto con un valor de departamento para cada empleado.  
  
 Para implementar seguridad dinámica, puede utilizar las siguientes funciones como parte de una fórmula DAX para devolver el nombre del usuario que ha iniciado sesión actualmente, o la propiedad CustomData en una cadena de conexión:  
  
|Función|Description|  
|--------------|-----------------|  
|[Función USERNAME (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)|Devuelve el dominio\nombredeusuario del usuario que ha iniciado sesión actualmente.|  
|[Función CUSTOMDATA (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)|Devuelve la propiedad CustomData en una cadena de conexión.|  
  
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
  
##  <a name="bkmk_testroles"></a> Testing roles  
 Al crear un proyecto de modelos, puede usar la característica Analizar en Excel para probar la eficacia de los roles que ha definido. En el menú **Modelo** del diseñador de modelos, al hacer clic en **Analizar en Excel**, y antes de que se inicie Excel, aparecerá el cuadro de diálogo **Elegir credenciales y perspectivas** . En este cuadro de diálogo, puede especificar el nombre de usuario actual, otro nombre de usuario, un rol y una perspectiva que usará para conectar con el modelo del área de trabajo como un origen de datos. Para obtener más información, consulte [analizar en Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|Tema|Description|  
|-----------|-----------------|  
|[Crear y administrar roles](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)|Las tareas de este tema explican cómo crear y administrar roles mediante el cuadro de diálogo **Administrador de roles** del diseñador de modelos.|  
  
## <a name="see-also"></a>Vea también  
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Analizar en Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [Función USERNAME (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [Función LOOKUPVALUE (DAX)](http://msdn.microsoft.com/en-us/73a51c4d-131c-4c33-a139-b1342d10caab)   
 [Función CUSTOMDATA (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
