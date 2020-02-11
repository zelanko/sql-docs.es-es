---
title: Iniciar la utilidad del símbolo del sistema dta y optimizar una carga de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: f34a5acf-1f3b-4484-a770-6470cb925ab0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf882bc731c8e435de808092e990b35ad23ce57e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110155"
---
# <a name="starting-the-dta-command-prompt-utility-and-tuning-a-workload"></a>Iniciar la utilidad del símbolo del sistema dta y optimizar una carga de trabajo
  Esta tarea le guía por los pasos para iniciar la utilidad **DTA** , ver su ayuda y usarla para optimizar una carga de trabajo desde el símbolo del sistema. Usa la carga de trabajo, script. SQL, que creó para la Asistente para la optimización de motor de base de datos práctica de la interfaz gráfica de usuario (GUI) para [optimizar una carga de trabajo](lesson-1-1-tuning-a-workload.md).  
  
 En este tutorial se usa la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Por motivos de seguridad, las bases de datos de ejemplo no se instalan de manera predeterminada. Para instalarlas, consulte [Instalar ejemplos de SQL Server y bases de datos de ejemplo](http://sqlserversamples.codeplex.com).  
  
 Las tareas siguientes le guían por los pasos necesarios para abrir un símbolo del sistema, iniciar la utilidad **dta** , ver la Ayuda de la sintaxis y optimizar una carga de trabajo sencilla (MyScript.sql) que ha creado en [Optimizar una carga de trabajo](lesson-1-1-tuning-a-workload.md).  
  
### <a name="to-start-the-dta-command-prompt-utility-and-view-help"></a>Para iniciar la utilidad del símbolo del sistema dta y ver la Ayuda  
  
1.  En el menú **Inicio** , seleccione **Todos los programas**, **Accesorios**y, después, haga clic en **Símbolo del sistema**.  
  
2.  En el símbolo del sistema, escriba lo siguiente y presione ENTRAR:  
  
    ```  
    dta -? | more  
    ```  
  
     La parte `| more` de este comando es opcional. No obstante, si la utiliza, puede examinar la ayuda de la sintaxis para la utilidad. Presione ENTRAR para avanzar por el texto de ayuda línea a línea o la BARRA ESPACIADORA para avanzar página a página.  
  
### <a name="to-tune-a-simple-workload-by-using-the-dta-command-prompt-utility"></a>Optimizar una carga de trabajo sencilla mediante la utilidad del símbolo del sistema dta  
  
1.  En el símbolo del sistema, navegue al directorio donde haya almacenado el archivo MyScript.sql.  
  
2.  En el símbolo del sistema, escriba lo siguiente y presione ENTRAR para ejecutar el comando e iniciar la sesión de optimización (observe que la utilidad reconoce mayúsculas y minúsculas al analizar comandos):  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
     donde `-S` especifica el nombre del servidor y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] está instalada. El valor `-E` especifica que se desea utilizar una conexión de confianza para la instancia, lo cual es apropiado si piensa conectarse con una cuenta de dominio de Windows. El valor `-D` especifica la base de datos que desea optimizar, `-if` especifica el archivo de carga de trabajo, `-s` especifica el nombre de la sesión, `-of` especifica el archivo en el que desea que la herramienta escriba el script de recomendaciones [!INCLUDE[tsql](../../includes/tsql-md.md)] y `-ox` especifica el archivo en el que desea que la herramienta escriba las recomendaciones en formato XML. Los tres últimos modificadores especifican las opciones de optimización siguientes: `-fa IDX_IV` especifica que el Asistente para la optimización de motor de base de datos solo debe agregar índices (agrupados y no agrupados) y vistas indizadas; `-fp NONE` especifica que durante el análisis no se tendrá en cuenta ninguna estrategia de partición; y `-fk NONE` especifica que no se debe mantener ninguna estructura de diseño físico en la base de datos cuando el Asistente para la optimización de motor de base de datos haga sus recomendaciones.  
  
3.  Una vez que el Asistente para la optimización de motor de base de datos acabe de optimizar la carga de trabajo, mostrará un mensaje para indicar que la sesión de optimización finalizó correctamente. Puede ver los resultados de la optimización utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para abrir los archivos MySession2OutputScript.sql y MySession2Output.xml. También puede abrir la sesión de optimización MySession2 en la GUI del Asistente para la optimización de motor de base de datos y ver las recomendaciones e informes de la misma forma que ha hecho en [Ver recomendaciones de optimización](lesson-1-2-viewing-tuning-recommendations.md) y [Ver informes de optimización](lesson-1-3-viewing-tuning-reports.md).  
  
## <a name="summary"></a>Resumen  
 Ha completado la optimización de una carga de trabajo sencilla desde el símbolo del sistema mediante la utilidad **dta** . Esta herramienta proporciona muchas otras opciones de optimización. Vea la Ayuda de la herramienta (**dta -?**) y el tema de referencia [dta (utilidad)](dta-utility.md) para obtener más información.  
  
## <a name="after-you-finish-this-tutorial"></a>Al finalizar este tutorial  
 Cuando haya finalizado las lecciones de este tutorial, consulte los temas siguientes para obtener más información acerca del Asistente para la optimización de motor de base de datos:  
  
-   [Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md) para obtener descripciones sobre cómo realizar tareas con esta herramienta.  
  
-   [dta (utilidad)](dta-utility.md) para obtener material de referencia sobre la utilidad de símbolo del sistema y el archivo XML opcional que puede usar para controlar el funcionamiento de la utilidad.  
  
 Para volver al principio del tutorial, consulte [Tutorial: Asistente para la optimización de motor de base de datos](tutorial-database-engine-tuning-advisor.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tutoriales del motor de base de datos](../../relational-databases/database-engine-tutorials.md)  
  
  
