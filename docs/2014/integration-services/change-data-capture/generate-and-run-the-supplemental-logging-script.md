---
title: Generar y ejecutar el script de registro complementario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5bfbff70d29e2b7b18c82b323d3ab34a3c6c60e
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381532"
---
# <a name="generate-and-run-the-supplemental-logging-script"></a>Generar y ejecutar el script de registro complementario
  Use la página Configurar tablas para capturar cambios con el fin de ejecutar un script en la base de datos de origen de Oracle que configurará el registro complementario.  
  
 **Para ejecutar los scripts de registro complementario**  
  
 Haga clic en **Ejecutar script** para ejecutar el script de registro complementario en las tablas definidas para la instancia CDC. Este script indica a la base de datos de Oracle que escriba todas las columnas de interés en sus registros de transacciones al registrar operaciones UPDATE en tablas capturadas. Normalmente es un administrador del sistema de Oracle quien examina y ejecuta este script.  
  
 También puede ejecutar los scripts manualmente mediante SQL * Plus.  
  
 **Para ejecutar los scripts manualmente**  
  
 Haga clic en **Copiar** para pegar el script en el Portapapeles. Abra SQL* Plus y vaya al directorio donde se encuentra la base de datos de origen de Oracle. Pegue el script en SQL\*Plus para ejecutarlo.  
  
 Para guardar el script de registro complementario en un archivo de texto, haga clic en **Guardar como** y vaya hasta la ubicación donde desee guardar el archivo. Asigne un nombre al archivo y haga clic en **Guardar** para guardar el archivo.  
  
 Haga clic en **Siguiente** para [Generate Mirror Tables and CDC Capture Instances](generate-mirror-tables-and-cdc-capture-instances.md).  
  
## <a name="see-also"></a>Vea también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Revisar y generar scripts de registro complementario](review-and-generate-supplemental-logging-scripts.md)  
  
  
