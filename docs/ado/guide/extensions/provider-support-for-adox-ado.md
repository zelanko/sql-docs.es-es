---
title: Compatibilidad del proveedor con ADOX (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b28d606dc96df94845f95d8f26e21b1a83461f0f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="provider-support-for-adox-ado"></a>Compatibilidad del proveedor con ADOX (ADO)
Algunas características de ADOX no son compatibles, en función del proveedor de datos OLE DB. ADOX es totalmente compatible con la [proveedor OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). Las características no compatibles con el [proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), [proveedor Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md), o la [proveedor Microsoft OLE DB para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) son se enumeran en las tablas siguientes. ADOX no es compatible con cualquier otro proveedor de Microsoft OLE DB.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Proveedor Microsoft OLE DB para SQL Server  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|**Tablas** colección|Propiedades son de lectura/escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|**Vistas** colección|**Vistas** no se admite.|  
|**Procedimientos** colección|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Procedimiento** objeto|El **comando** propiedad no es compatible.|  
|**Las claves** colección|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Los usuarios** colección|**Los usuarios** no se admite.|  
|**Grupos de** colección|**Grupos** no se admite.|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Proveedor Microsoft OLE DB para ODBC  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|**Catálogo** objeto|El **Create** método no se admite.|  
|**Tablas** colección|El **anexado** y **eliminar** métodos no son compatibles. Propiedades son de lectura/escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|**Procedimientos** colección|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Procedimiento** objeto|El **comando** propiedad no es compatible.|  
|**Índices** colección|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Las claves** colección|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Los usuarios** colección|**Los usuarios** no se admite.|  
|**Grupos de** colección|**Grupos** no se admite.|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>proveedor Microsoft OLE DB para Oracle  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|**Catálogo** objeto|El **Create** método no se admite.|  
|**Tablas** colección|El **anexado** y **eliminar** métodos no son compatibles. Propiedades son de lectura/escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|**Vistas** colección|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Vista** objeto|El **comando** propiedad no es compatible.|  
|**Procedimientos** objeto|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Procedimiento** objeto|El **comando** propiedad no es compatible.|  
|**Índices** colección|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Las claves** colección|El **anexado** y **eliminar** métodos no son compatibles.|  
|**Los usuarios** colección|**Los usuarios** no se admite.|  
|**Grupos de** colección|**Grupos** no se admite.|
