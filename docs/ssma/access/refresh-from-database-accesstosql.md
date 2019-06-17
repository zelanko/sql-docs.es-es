---
title: Actualizar desde la base de datos (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3b671f49-c4cc-44fd-801e-e738a8c79415
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 29dd391a094f37334008e98af60bcdc2396a997a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63299117"
---
# <a name="refresh-from-database-accesstosql"></a>Actualizar desde la base de datos (AccessToSQL)
El **actualizar desde la base de datos** cuadro de diálogo le permite seleccionar los objetos que desea actualizar desde la base de datos de Access. Las filas en el cuadro de diálogo están codificados con colores según el estado de los metadatos:  
  
-   Si los metadatos del objeto ha cambiado localmente y en la base de datos de Access, la fila está en azul.  
  
-   Si los metadatos del objeto ha cambiado en la base de datos de Access, pero no en SSMA, la fila está en amarilla.  
  
-   Si los metadatos del objeto ha cambiado localmente, pero no en la base de datos de Access, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos de Access, la fila es de color fucsia.  
  
Puede especificar la configuración de actualización de objeto predeterminado en el **configuración del proyecto** cuadro de diálogo. Para obtener más información, consulte [configuración del proyecto &#40;cargar objetos&#41; &#40;AccessToSQL&#41;](../../ssma/access/project-settings-loading-objects-accesstosql.md)  
  
Para tener acceso a la **actualizar desde la base de datos** diálogo cuadro, haga clic en cualquier **base de datos** nodo en el Explorador de metadatos de acceso y haga clic en **actualizar desde la base de datos**.  
  
