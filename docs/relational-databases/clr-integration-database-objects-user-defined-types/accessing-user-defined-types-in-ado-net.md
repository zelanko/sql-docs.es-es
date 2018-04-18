---
title: Obtener acceso a tipos definidos por el usuario en ADO.NET | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
caps.latest.revision: 12
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a748da511a89bdfb97e22a2d07ca9d02dea73448
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="accessing-user-defined-types-in-adonet"></a>Obtener acceso a tipos definidos por el usuario en ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Tipos definidos por el usuario (UDT) se escriben con cualquiera de los idiomas admitidos por el [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework common language runtime (CLR) que genera código comprobable. Esto incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Los UDT permiten almacenar objetos y estructuras de datos personalizadas en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos se exponen como miembros públicos de una clase o estructura de .NET Framework y los comportamientos se definen mediante métodos de la clase o estructura. Un UDT puede utilizarse como definición de columna de una tabla, como una variable en un [!INCLUDE[tsql](../../includes/tsql-md.md)] lote, o como un argumento de un [!INCLUDE[tsql](../../includes/tsql-md.md)] función o procedimiento almacenado.  
  
 En ADO.NET, el **System.Data.SqlClient** proveedor expone los UDT de las maneras siguientes:  
  
-   A través de la **System.Data.SqlClient.SqlDataReader** como un objeto.  
  
-   A través de la **SqlDataReader** como bytes sin formato.  
  
-   Como un parámetro de un **System.Data.SqlClient.SqlParameter** objeto.  
  
## <a name="in-this-section"></a>En esta sección  
 [Recuperar datos UDT](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 Describe cómo recuperar los datos UDT y cómo especificar parámetros.  
  
 [Actualizar columnas de UDT con DataAdapters](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Describe cómo trabajar con UDT en **conjuntos de datos** y cómo actualizar datos UDT mediante **DataAdapters**.  
  
## <a name="see-also"></a>Vea también  
 [Tipos definidos por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
