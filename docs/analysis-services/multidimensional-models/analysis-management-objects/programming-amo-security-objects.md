---
title: Programar objetos de seguridad AMO | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, security
- AMO, security
ms.assetid: 5d963721-6e6e-46eb-bc9b-18724dd0b751
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f77d58eeaef6b127492f9944e15f0b751f03d704
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="programming-amo-security-objects"></a>Programar objetos de seguridad AMO
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]En [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], programar objetos de seguridad o ejecutar aplicaciones que usan objetos de seguridad AMO requiere ser miembro del grupo Administrador del servidor o el grupo de administradores de base de datos. Administrador del servidor y Administrador de base de datos son un acceso niveles proporcionado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 En [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], el acceso de usuario a cualquier objeto se obtiene a través de la combinación de roles y permisos que se asignan a ese objeto. Para obtener más información, consulte [clases Security de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md).  
  
## <a name="role-and-permission-objects"></a>Objetos de rol y permiso  
 Los roles del servidor contienen un único rol en la colección, el rol de los administradores. Los nuevos roles no se pueden agregar a la colección de roles del servidor. La pertenencia en el rol de los administradores permite el acceso completo a cada objeto del servidor  
  
 Los objetos <xref:Microsoft.AnalysisServices.Role> se crean en el nivel de base de datos. El mantenimiento del rol requiere únicamente agregar o quitar miembros al rol o del rol, así como agregar o quitar roles al objeto <xref:Microsoft.AnalysisServices.Database>. Un rol no se puede quitar si es cualquier objeto <xref:Microsoft.AnalysisServices.Permission> asociado al rol. Para quitar un rol, se deben buscar todos los objetos <xref:Microsoft.AnalysisServices.Permission> en los objetos <xref:Microsoft.AnalysisServices.Database> y quitar los permisos de <xref:Microsoft.AnalysisServices.Role>, antes de que <xref:Microsoft.AnalysisServices.Role> se quite de <xref:Microsoft.AnalysisServices.Database>.  
  
 Los permisos definen las acciones habilitadas en el objeto donde se proporciona el permiso. Se pueden proporcionar permisos a los objetos siguientes: <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MiningStructure>y <xref:Microsoft.AnalysisServices.MiningModel>. El mantenimiento del permiso implica conceder o revocar acceso habilitado por la propiedad de acceso correspondiente. Para cada acceso habilitado, hay una propiedad que se puede establecer en el nivel de acceso que se desee. El acceso se puede definir para las operaciones siguientes: Procesar, leer definición, leer, escribir y administrar. Administrar el acceso únicamente se define en el objeto <xref:Microsoft.AnalysisServices.Database>. Se obtiene el nivel de seguridad del administrador de bases de datos cuando se concede el rol con el permiso para administrar la base de datos.  
  
 En el ejemplo siguiente crea cuatro roles: Los administradores de bases de datos, procesadores, escritores y lectores.  
  
 Los administradores de bases de datos pueden administrar la base de datos proporcionada.  
  
 Los procesadores pueden procesar todos los objetos en una base de datos y comprobar los resultados. Para comprobar los resultados, se debe habilitar explícitamente al cubo proporcionado el acceso de lectura al objeto de la base de datos, porque el permiso de lectura no se aplica a objetos secundarios.  
  
 Los escritores pueden leer y escribir al cubo proporcionado y el acceso a celdas se limita a la dimensión del cliente en 'United States'.  
  
 Los lectores pueden leer en el cubo proporcionado y el acceso a celdas se limita a la dimensión del cliente en 'United States'.  
  
```  
static public void CreateRolesAndPermissions(Database db, Cube cube)  
{  
    Role role;  
    DatabasePermission dbperm;  
    CubePermission cubeperm;  
  
    #region Create the Database Administrators role  
  
    // Create the Database Administrators role.  
    role = db.Roles.Add("Database Administrators");  
    role.Members.Add(new RoleMember("")); // e.g. domain\user  
    role.Update();  
  
    // Assign administrative permissions to this role.  
    // Members of this role can perform any operation within the database.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Administer = true;  
    dbperm.Update();  
  
    #endregion  
  
    #region Create the Processors role  
  
    // Create the Processors role.  
    role = db.Roles.Add("Processors");  
    role.Members.Add(new RoleMember("")); // e.g. myDomain\johndoe  
    role.Update();  
  
    // Assign Read and Process permissions to this role.  
    // Members of this role can process objects in the database and query them to verify results.  
    // Process permission applies to all contained objects, i.e. all dimensions and cubes.  
    // Read permission does not apply to contained objects, so we must assign the permission explicitly on the cubes.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Process = true;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Writers role  
  
    // Create the Writers role.  
    role = db.Roles.Add("Writers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read and Write permissions to this role.  
    // Members of this role can discover, query and writeback to the Adventure Works cube.  
    // However cell access and writeback is restricted to the United States (in the Customer dimension).  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Write = WriteAccess.Allowed;  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.Read, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.ReadWrite, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Readers role  
  
    // Create the Readers role.  
    role = db.Roles.Add("Readers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read permissions to this role.  
    // Members of this role can discover and query the Adventure Works cube.  
    // However the Customer dimension is restricted to the United States.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    Dimension dim = db.Dimensions.GetByName("Customer");  
    DimensionAttribute attr = dim.Attributes.GetByName("Country-Region");  
    CubeDimensionPermission cubedimperm = cubeperm.DimensionPermissions.Add(dim.ID);  
    cubedimperm.Read = ReadAccess.Allowed;  
    AttributePermission attrperm = cubedimperm.AttributePermissions.Add(attr.ID);  
    attrperm.AllowedSet = "{[Customer].[Country-Region].[Country-Region].&[United States]}";  
    cubeperm.Update();  
  
    #endregion  
}  
```  
  
## <a name="see-also"></a>Ver también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programar objetos de seguridad de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [Permisos y derechos de acceso &#40; Analysis Services - datos multidimensionales &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Arquitectura lógica &#40; Analysis Services - datos multidimensionales &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos &#40; Analysis Services - datos multidimensionales &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
