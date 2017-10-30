---
title: "Los pasos de la importación de SQL Server y el Asistente para exportación | Documentos de Microsoft"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 22d1f4b78fadab6d7b6659104b54a564f11da308
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>Pasos de la importación de SQL Server y el Asistente para exportación
Este tema describe la secuencia de pasos para importar y exportar datos con la importación de SQL Server y el Asistente para exportación. También contiene vínculos a las páginas individuales de documentación que describe cada página o cuadro de diálogo que se ven en el asistente.

Este tema se describe sólo la **pasos** en el asistente. Si está buscando algo, consulte [relacionados con tareas y contenido](#related).

## <a name="steps-for-importing-and-exporting-data"></a>Pasos para importar y exportar datos  
 En la tabla siguiente se muestran los pasos para importar y exportar los datos, así como las páginas correspondientes del asistente. Según las opciones que seleccione en el asistente, normalmente no ve todas estas páginas.  

Para obtener una visión rápida de las varias pantallas que ve en una sesión típica, eche un vistazo en este sencillo ejemplo de extremo a extremo en una sola página - [empezar a trabajar con este ejemplo sencillo de la importación y el Asistente para exportación de](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

|Paso|Páginas del asistente|  
|----------|------------------|  
|**Bienvenida**<br />No hace falta que realice ninguna acción en esta página.|[Asistente para importar y exportar de SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**Elija el origen** de los datos.|[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)|  
|**Elija el destino** de los datos.|[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)|  
|**Configurar el destino de**. (pasos opcionales)<br /><br /> -   Cree una base de datos de destino.<br />-   Si está copiando datos a un archivo de texto, configure las opciones adicionales.|[Crear base de datos](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[Configurar el destino de archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**Especificar lo que van a copiar.**|[Especificar copia de tabla o consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[Seleccionar tablas de origen y vistas](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[Proporcionar una consulta de origen](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**Configurar la operación de copia**. (pasos opcionales)<br /><br /> -   Cree una tabla de destino.<br />-Decidir qué hacer si el asistente no sabe cómo asignar tipos de datos entre el origen y destino que ha seleccionado.<br />-   Revise la asignación de columnas entre el origen y el destino.<br />-   Solucione los problemas de la conversión de tipos de datos entre el origen y el destino.<br />-   Obtenga una vista previa de los datos que se van a copiar.|[Instrucción Create Table de SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[Convertir a tipos sin comprobar conversión](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[Cuadro de diálogo Detalles de conversión de columna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[Cuadro de diálogo de vista previa de datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**Copie los datos.**<br /><br /> Si lo desea, guarde la configuración como un paquete de SQL Server Integration Services (SSIS).|[Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[Complete el Asistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[Realizar la operación](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> Pulse la tecla F1 en cualquier página o cuadro de diálogo del Asistente para ver la documentación de la página actual.

## <a name="related"></a>Contenido y las tareas relacionadas  
A continuación, presentamos algunas otras tareas básicas.
-   **Vea un ejemplo rápido de cómo funciona el asistente.**

    -   **Si prefiere ver capturas de pantalla.** Eche un vistazo a este sencillo ejemplo de extremo a extremo en una sola página - [empezar a trabajar con este ejemplo sencillo de la importación y el Asistente para exportación de](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Si prefiere ver un vídeo.** Vea este vídeo de cuatro minutos desde YouTube que muestra el asistente y se explica con claridad y simplemente cómo exportar datos a Excel - [mediante la importación de SQL Server y el Asistente para exportación para exportar a Excel](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Más información sobre cómo funciona el asistente.**

    -   **Más información sobre el asistente.** Si quiere obtener información general sobre el asistente, consulte [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Obtenga información acerca de cómo conectarse a orígenes de datos y destinos.** Si desea obtener información acerca de cómo conectarse a los datos, seleccione la página que desee en la lista aquí - [conectar a orígenes de datos con la importación de SQL Server y el Asistente para exportación de](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md). Hay una página independiente de la documentación de cada uno de varios orígenes de datos de uso frecuente. 

-   **Inicie al asistente.** Si está listo para ejecutar el asistente y simplemente quiere saber cómo iniciarlo, consulte [Iniciar el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

-     **Obtenga el asistente** Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).



