---
title: Actualizar desde la base de datos (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3b671f49-c4cc-44fd-801e-e738a8c79415
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 06174be45e178f3fb7c612925e78795bf4eeaa7c
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933931"
---
# <a name="refresh-from-database-accesstosql"></a>Actualizar desde la base de datos (AccessToSQL)
El cuadro de diálogo **actualizar desde base de datos** permite seleccionar los objetos que se van a actualizar desde la base de datos de Access. Las filas del cuadro de diálogo están codificadas por colores en función del estado de los metadatos:  
  
-   Si los metadatos del objeto han cambiado localmente y en la base de datos de Access, la fila es azul.  
  
-   Si los metadatos del objeto han cambiado en la base de datos de Access pero no en SSMA, la fila es amarilla.  
  
-   Si los metadatos del objeto han cambiado localmente, pero no en la base de datos de Access, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos de Access, la fila es de color rosa.  
  
Puede especificar la configuración de actualización de objetos predeterminada en el cuadro de diálogo **configuración del proyecto** . Para obtener más información, vea [configuración del proyecto &#40;cargar objetos&#41; &#40;AccessToSQL&#41;](../../ssma/access/project-settings-loading-objects-accesstosql.md)  
  
Para tener acceso al cuadro **de diálogo actualizar desde base** de datos, haga clic con el botón secundario en cualquier nodo de **base** de datos en el explorador de metadatos y haga clic en **actualizar desde base de**datos  
  
