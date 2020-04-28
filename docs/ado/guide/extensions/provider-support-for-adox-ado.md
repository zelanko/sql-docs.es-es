---
title: Compatibilidad del proveedor con ADOX (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX provider support [ADO]
ms.assetid: 64234ce5-dc46-4c8a-a316-61956b6b9abb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b07f4563d54254310c08c8c132d0729b8ccdc6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923216"
---
# <a name="provider-support-for-adox-ado"></a>Compatibilidad del proveedor con ADOX (ADO)
Ciertas características de ADOX no se admiten, en función del proveedor de datos de OLE DB. ADOX es totalmente compatible con el [proveedor de OLE DB para Microsoft Jet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-jet.md). En las tablas siguientes se enumeran las características no admitidas con el [proveedor de microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), el [proveedor de Microsoft OLE DB para ODBC](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-odbc.md)o el [proveedor OLE DB de Microsoft para Oracle](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-oracle.md) . ADOX no es compatible con ningún otro proveedor de Microsoft OLE DB.  
  
## <a name="microsoft-ole-db-provider-for-sql-server"></a>Proveedor OLE DB de Microsoft para SQL Server  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|Colección de **tablas**|Las propiedades son de lectura y escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|Colección de **vistas**|No se admiten **vistas** .|  
|Colección de **procedimientos**|No se admiten los métodos **Append** y **Delete** .|  
|**Procedure** (objeto)|No se admite la propiedad **Command** .|  
|Colección de **claves**|No se admiten los métodos **Append** y **Delete** .|  
|Recopilación de **usuarios**|No se admiten **usuarios** .|  
|Colección de **grupos**|No se admiten **grupos** .|  
  
## <a name="microsoft-ole-db-provider-for-odbc"></a>Proveedor Microsoft OLE DB para ODBC  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|Objeto de **Catálogo**|No se admite el método **Create** .|  
|Colección de **tablas**|No se admiten los métodos **Append** y **Delete** . Las propiedades son de lectura y escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|Colección de **procedimientos**|No se admiten los métodos **Append** y **Delete** .|  
|**Procedure** (objeto)|No se admite la propiedad **Command** .|  
|Colección de **índices**|No se admiten los métodos **Append** y **Delete** .|  
|Colección de **claves**|No se admiten los métodos **Append** y **Delete** .|  
|Recopilación de **usuarios**|No se admiten **usuarios** .|  
|Colección de **grupos**|No se admiten **grupos** .|  
  
## <a name="microsoft-ole-db-provider-for-oracle"></a>proveedor Microsoft OLE DB para Oracle  
  
|Objeto o colección|Restricción de uso|  
|--------------------------|-----------------------|  
|Objeto de **Catálogo**|No se admite el método **Create** .|  
|Colección de **tablas**|No se admiten los métodos **Append** y **Delete** . Las propiedades son de lectura y escritura antes de la creación de objetos y de solo lectura cuando se hace referencia a un objeto existente.|  
|Colección de **vistas**|No se admiten los métodos **Append** y **Delete** .|  
|Objeto de **vista**|No se admite la propiedad **Command** .|  
|**Procedures** (objeto)|No se admiten los métodos **Append** y **Delete** .|  
|**Procedure** (objeto)|No se admite la propiedad **Command** .|  
|Colección de **índices**|No se admiten los métodos **Append** y **Delete** .|  
|Colección de **claves**|No se admiten los métodos **Append** y **Delete** .|  
|Recopilación de **usuarios**|No se admiten **usuarios** .|  
|Colección de **grupos**|No se admiten **grupos** .|
