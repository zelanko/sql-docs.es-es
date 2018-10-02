---
title: Pasos del Asistente para importación y exportación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 816fb1bd-7bb9-450d-ad65-e4c2d02eaff8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 73b43cd2f14f8c7afd531a295d9eaf118d5e91d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694163"
---
# <a name="steps-in-the-sql-server-import-and-export-wizard"></a>Pasos del Asistente para importación y exportación de SQL Server
En este tema se describe la secuencia de pasos para importar y exportar datos con el Asistente para importación y exportación de SQL Server. También contiene vínculos a páginas individuales de documentación, que describen cada página o cuadro de diálogo que muestra el asistente.

En este tema se describen solo los **pasos** del asistente. Si busca algo más, consulte [Temas y tareas relacionados](#related).

## <a name="steps-for-importing-and-exporting-data"></a>Pasos para la importación y exportación de datos  
 En la tabla siguiente se muestran los pasos para importar y exportar los datos, así como las páginas correspondientes del asistente. Según las opciones que seleccione en el asistente, podría no ver todas estas páginas.  

Para obtener una visión rápida de las distintas pantallas que se muestran en una sesión típica, eche un vistazo a este sencillo y completo ejemplo en una sola página: [Comenzar con este sencillo ejemplo del Asistente para importación y exportación](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

|Paso|Páginas del asistente|  
|----------|------------------|  
|**Bienvenida**<br />No es necesario que realice ninguna acción en esta página.|[Asistente para importar y exportar de SQL Server](../../integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)|  
|**Elija el origen** de los datos.|[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos)|  
|**Elija el destino** de los datos.|[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino)|  
|**Configure el destino**. (Pasos opcionales)<br /><br /> -   Cree una base de datos de destino.<br />-   Si está copiando datos a un archivo de texto, configure las opciones adicionales.|[Crear base de datos](../../integration-services/import-export-data/create-database-sql-server-import-and-export-wizard.md)<br /><br />[Configurar el destino del archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)|  
|**Especifique lo que quiere copiar.**|[Especificar copia de tabla o consulta](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md)<br /><br />[Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)<br /><br />[Proporcionar una consulta de origen](../../integration-services/import-export-data/provide-a-source-query-sql-server-import-and-export-wizard.md)|  
|**Configure la operación de copia**. (Pasos opcionales)<br /><br /> -   Cree una tabla de destino.<br />-   Decida qué hacer si el asistente no sabe cómo asignar tipos de datos entre el origen y el destino que ha seleccionado.<br />-   Revise la asignación de columnas entre el origen y el destino.<br />-   Solucione los problemas de la conversión de tipos de datos entre el origen y el destino.<br />-   Obtenga una vista previa de los datos que se van a copiar.|[Instrucción Create Table de SQL](../../integration-services/import-export-data/create-table-sql-statement-sql-server-import-and-export-wizard.md)<br /><br />[Convertir tipos sin comprobar conversión](../../integration-services/import-export-data/convert-types-without-conversion-checking-sql-server-import-and-export-wizard.md)<br /><br />[Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)<br /><br />[Revisar asignación de tipos de datos](../../integration-services/import-export-data/review-data-type-mapping-sql-server-import-and-export-wizard.md)<br /><br />[Cuadro de diálogo Detalles de conversión de columna](../../integration-services/import-export-data/column-conversion-details-dialog-box-sql-server-import-and-export-wizard.md)<br /><br />[Cuadro de diálogo Vista previa de los datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md)|  
|**Copie los datos.**<br /><br /> Si lo desea, guarde la configuración como un paquete de SQL Server Integration Services (SSIS).|[Guardar y ejecutar el paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)<br /><br />[Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)<br /><br />[Finalización del asistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)<br /><br />[Operación en curso](../../integration-services/import-export-data/performing-operation-sql-server-import-and-export-wizard.md)|  

> [!TIP]
> Pulse la tecla F1 en cualquier página o cuadro de diálogo del Asistente para ver la documentación de la página actual.

## <a name="related"></a> Temas y tareas relacionados  
A continuación, se presentan algunas tareas básicas adicionales.
-   **Vea un ejemplo rápido de cómo funciona el asistente.**

    -   **Si prefiere ver capturas de pantalla.** Eche un vistazo a este ejemplo sencillo y completo en una sola página: [Get started with this simple example of the Import and Export Wizard (Comenzar con este sencillo ejemplo del Asistente para importación y exportación)](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).

    -   **Si prefiere ver un vídeo.** Aquí tiene un vídeo de cuatro minutos de YouTube en el que se muestra el asistente y se explica cómo exportar datos a Excel, con instrucciones claras y sencillas: [Using the SQL Server Import and Export Wizard to Export to Excel (Usar el Asistente para importación y exportación de SQL Server para exportar a Excel)](https://go.microsoft.com/fwlink/?linkid=829049).

-   **Obtenga más información sobre cómo funciona el asistente.**

    -   **Obtenga más información sobre el asistente.** Si quiere obtener información general sobre el asistente, consulte [Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

    -   **Obtenga información sobre cómo conectarse a orígenes y destinos de datos.** Si está buscando información sobre cómo conectarse a sus datos, seleccione la página que quiera de esta lista: [Connect to data sources with the SQL Server Import and Export Wizard](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md) (Conexión a orígenes de datos con el Asistente para importación y exportación de SQL Server). Hay una página independiente de documentación para cada uno de los varios orígenes de datos de uso frecuente. 

-   **Inicie el asistente.** Si está listo para ejecutar el asistente y simplemente quiere saber cómo iniciarlo, consulte [Iniciar el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

-     **Obtenga el asistente** Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).


