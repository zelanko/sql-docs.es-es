---
title: Cómo editar las propiedades de la instancia de CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96604a09811626a304502dc05ef4f7e9edcd0359
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771233"
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>Cómo editar las propiedades de la instancia CDC
  En este procedimiento se describe cómo usar la Consola del diseñador CDC para editar las propiedades de configuración de una instancia CDC.  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>Para editar las propiedades de configuración de la instancia CDC  
  
1.  En el menú **Inicio** , seleccione **Consola del diseñador CDC**.  
  
2.  En el panel izquierdo, expanda **Captura de datos modificados** y expanda después el servicio que contiene la instancia cuyas propiedades desea editar.  
  
3.  Seleccione el nombre de la instancia cuyas propiedades desea editar.  
  
4.  En el panel Acciones situado en el lado derecho de la Consola del diseñador CDC, haga clic en **Propiedades**.  
  
     También puede hacer clic con el botón derecho en la instancia cuyas propiedades quiere editar y luego hacer clic en **Propiedades**.  
  
5.  En el editor de propiedades, edite las propiedades en las pestañas siguientes:  
  
    -   **Oracle**: use la pestaña **Oracle** del editor de propiedades para realizar cambios en la descripción que proporcionó en la página de creación de la base de datos CDC del Asistente para nueva instancia y para realizar cambios en la información de conexión a bases de datos de minería de registros de Oracle.  
  
         Para obtener información acerca de lo que puede editar en esta pestaña, vea [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md).  
  
    -   **Tablas**: Use la pestaña **Tablas** para realizar cambios en las tablas y columnas que seleccionó en la base de datos de origen de Oracle.  
  
         Para obtener información acerca de lo que puede editar en esta pestaña, vea [Edit Tables](edit-tables.md).  
  
    -   **Scripts**: use la pestaña **Scripts** para ejecutar o volver a ejecutar un script en la base de datos de origen de Oracle que configurará el registro complementario.  
  
         Para obtener información acerca de lo que puede hacer en esta pestaña, vea [Review and Generate Supplemental Logging Scripts](review-and-generate-supplemental-logging-scripts.md).  
  
    -   **Avanzadas**: Use la pestaña **Avanzadas** para agregar propiedades especiales a la instancia CDC.  
  
         Para obtener información acerca de lo que puede hacer en esta pestaña, vea [Edit the Advanced Properties](edit-the-advanced-properties.md).  
  
  
