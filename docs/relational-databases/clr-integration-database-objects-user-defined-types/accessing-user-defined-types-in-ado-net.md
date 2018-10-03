---
title: Acceso a tipos definidos por el usuario en ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 82ccd420318026bddac2979735c514b8b43e4a88
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631093"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Obtener acceso a tipos definidos por el usuario en ADO.NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Tipos definidos por el usuario (UDT) se escriben con cualquiera de los idiomas admitidos por el [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework common language runtime (CLR) que genera código comprobable. Esto incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# y [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Los UDT permiten almacenar objetos y estructuras de datos personalizadas en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos se exponen como miembros públicos de una clase o estructura de .NET Framework y los comportamientos se definen mediante métodos de la clase o estructura. Un UDT puede usarse como la definición de columna de una tabla, como una variable de un lote [!INCLUDE[tsql](../../includes/tsql-md.md)] o como un argumento de una función o procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
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
 [Tipos definidos por el usuario de CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
