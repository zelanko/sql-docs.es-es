---
title: Cómo editar las propiedades de la instancia de CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b2d15f17b867cd02d700ce6c749edddaa2c65083
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772947"
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
  
    -   **Oracle**: Use la **Oracle** ficha en el editor de propiedades para realizar cambios en la descripción que proporcionó en la página de base de datos CDC crear en el Asistente para nueva instancia y para realizar cambios en la información de conexión de base de datos Oracle Log Mining.  
  
         Para obtener información acerca de lo que puede editar en esta pestaña, vea [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md).  
  
    -   **Las tablas**: Use la pestaña **Tablas** para realizar cambios en las tablas y columnas que seleccionó en la base de datos de origen de Oracle.  
  
         Para obtener información acerca de lo que puede editar en esta pestaña, vea [Edit Tables](edit-tables.md).  
  
    -   **Las secuencias de comandos**: Use la **Scripts** tab para ejecutar o volver a ejecutar una secuencia de comandos en la base de datos de origen de Oracle que configurará el registro complementario.  
  
         Para obtener información acerca de lo que puede hacer en esta pestaña, vea [Review and Generate Supplemental Logging Scripts](review-and-generate-supplemental-logging-scripts.md).  
  
    -   **Avanzadas**: Use la pestaña **Avanzadas** para agregar propiedades especiales a la instancia CDC.  
  
         Para obtener información acerca de lo que puede hacer en esta pestaña, vea [Edit the Advanced Properties](edit-the-advanced-properties.md).  
  
  
