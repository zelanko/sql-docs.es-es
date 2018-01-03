---
title: "Append (método) (usuarios ADOX) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords: Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69f839a24ee99d0db10435a3562926786f2d4620
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="append-method-adox-users"></a>Append (método) (usuarios ADOX)
Agrega un nuevo [usuario](../../../ado/reference/adox-api/user-object-adox.md) el objeto a la [usuarios](../../../ado/reference/adox-api/users-collection-adox.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Usuario*  
 A **Variant** valor que contiene el **usuario** objeto que se anexará o el nombre del usuario que se va a crear y anexar.  
  
 *Contraseña*  
 Opcional. A **cadena** valor que contiene la contraseña para el usuario. El *contraseña* parámetro corresponde al valor especificado por el [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) método de un **usuario** objeto.  
  
## <a name="remarks"></a>Comentarios  
 El **usuarios** colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa a los usuarios de todos los del catálogo. El **usuarios** colección para un [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa sólo los usuarios que tienen una pertenencia al grupo específico.  
  
 Se producirá un error si el proveedor no admite la creación de usuarios.  
  
> [!NOTE]
>  Antes de anexar una **usuario** el objeto a la **usuarios** colección de un **grupo** objeto, un **usuario** objeto con el mismo [nombre ](../../../ado/reference/adox-api/name-property-adox.md) tal y como lo que se debe anexar ya debe existir en el **usuarios** colección de la **catálogo**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Vea también  
 [Los usuarios y grupos, ChangePassword ejemplo de métodos Append (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append (método) (columnas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append (método) (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append (método) (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append (método) (claves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append (método) (ADOX procedimientos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append (método) (tablas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append (método) (vistas ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
