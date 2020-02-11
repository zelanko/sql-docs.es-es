---
title: Objetos creados en el publicador de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], objects created
ms.assetid: c58a124b-4da7-46e2-9292-af8ce9e6664b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99e1d1f0692e5460e2c7003b0ab8dca860deca4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63022146"
---
# <a name="objects-created-on-the-oracle-publisher"></a>Objects Created on the Oracle Publisher
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la replicación instala objetos de base de datos en el publicador de Oracle para habilitar el[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seguimiento y el reenvío de cambios (no instala ningún archivo binario en el publicador de Oracle). En la siguiente tabla se muestran los objetos que se crean en el publicador de Oracle cuando se identifica como publicador en el distribuidor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Las descripciones de los objetos se proporcionan solo como información. Estos objetos no se deben modificar.  
  
|Nombre de objeto|Tipo de objeto|Descripción|  
|-----------------|-----------------|-----------------|  
|HREPL_ArticleNlog_V|Tabla|Tabla de seguimiento de cambios que se utiliza para almacenar información cuando se realizan cambios en la tabla publicada. Se crea una tabla de seguimiento de cambios para cada tabla publicada.|  
|HREPL_Changes|Tabla|Tabla utilizada internamente por el trabajo Xactset para determinar el número de cambios que esperan ser asignados a un conjunto de transacciones. Para obtener más información sobre este trabajo, consulte [Optimizar el rendimiento de publicadores de Oracle](performance-tuning-for-oracle-publishers.md).|  
|HREPL_Distributor|Tabla|Tabla de estado del distribuidor que se utiliza para mantener información acerca del distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asociado con el publicador de Oracle.|  
|HREPL_Event|Tabla|Tabla de eventos que se utiliza para sincronizar instantáneas y solicitudes de recuento de filas.|  
|HREPL_Mutex|Tabla|Tabla que se utiliza para garantizar que el procedimiento de paquetes de Oracle PopulatePollTable no se ejecute simultáneamente por el Agente de registro del LOG y el trabajo de la base de datos.|  
|HREPL_Poll|Tabla|Tabla que se utiliza para identificar las entradas de la tabla de registro asociadas con conjuntos de cambios en las tablas publicadas.|  
|HREPL_PublishedTables|Tabla|Tabla que contiene una entrada para cada artículo en una publicación transaccional.|  
|HREPL_Publisher|Tabla|Tabla de estado del publicador que se utiliza para mantener información específica del publicador.|  
|HREPL_SchemaFilter|Tabla|Tabla que contiene esquemas que no se muestran cuando se publica a través del Asistente para nueva publicación.|  
|HREPL_XactsetCreateTimes|Tabla|Tabla que identifica la hora de creación asociada con cada conjunto de transacciones.|  
|HREPL_XactsetJob|Tabla|Tabla con la configuración de parámetros actual para el trabajo Xactset.|  
|HREPL_Pollid|Secuencia|Secuencia que se utiliza para generar Id. de sondeo.|  
|HREPL_Seq|Secuencia|Secuencia que se utiliza para ordenar comandos de cambio.|  
|HREPL_Stmt|Secuencia|Secuencia que se utiliza para generar Id. de instrucción.|  
|HREPL|Paquete y cuerpo del paquete|Paquete de códigos de compatibilidad con el publicador que se crea en el publicador.|  
|MSSQLSERVERDISTRIBUTOR|Sinónimo público|Sinónimo público para la tabla HREPL_Distributor. Si configura un distribuidor para utilizarlo con un publicador de Oracle y ya existe este sinónimo en la base de datos, se quitará y se volverá a crear.<br /><br /> Al quitar el sinónimo público y el usuario configurado de la replicación de Oracle con la opción CASCADE, se quitan todos los objetos de replicación del publicador de Oracle.|  
|HREPL_Len_I_J_K|Función|Función definida fuera del código del paquete de publicación de Oracle, que se utiliza para consultar la longitud de una columna LONG (utilizada al generar comandos con parámetros para las tablas con columnas LONG publicadas). Se crea una función para cada tabla publicada con una columna LONG.|  
|HREPL_DropPublisher|Procedimiento|Procedimiento definido fuera del código del paquete de publicación de Oracle, que se utiliza para quitar el publicador de Oracle.|  
|HREPL_ExecuteCommand|Procedimiento|Procedimiento definido fuera del código del paquete de publicación de Oracle, que se utiliza para ejecutar un comando en el publicador.|  
|HREPL_ArticleN_Trigger_Row|Desencadenador|Desencadenador generado para cada tabla publicada, que se utiliza para realizar un seguimiento de los cambios de fila.|  
|HREPL_ArticleN_Trigger_Stmt|Desencadenador|Desencadenador generado para cada tabla publicada, que se utiliza para realizar un seguimiento de los cambios de nivel de instrucción.|  
|HREPL_Article_I_J|Ver|Vista creada para cada tabla publicada, que se utiliza para realizar consultas en la tabla publicada.|  
|HREPL_Log_I_J_K|Ver|Vista creada para cada tabla publicada, que se utiliza para realizar consultas en la tabla de seguimiento de cambios.|  
  
## <a name="see-also"></a>Consulte también  
 [Configurar un publicador de Oracle](configure-an-oracle-publisher.md)   
 [Glosario de términos de publicaciones de Oracle](glossary-of-terms-for-oracle-publishing.md)   
 [Información general de la publicación de Oracle](oracle-publishing-overview.md)  
  
  
