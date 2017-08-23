---
title: "Información general: Exportar datos a Excel (agregar de MDS para Excel) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b628548b-982b-4e45-abf4-c8e83e3ab1c2
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3a005373e8785d679b127f3a7e85f974351d40a8
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="overview-exporting-data-to-excel-mds-add-in-for-excel"></a>Overview: Exporting Data to Excel (MDS Add-in for Excel)
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], debe exportar los datos del repositorio MDS a una hoja de cálculo de Excel activa para poder trabajar con ellos. Cuando termine de trabajar con los datos, impórtelos en el repositorio MDS para que otros usuarios puedan compartirlos.  
  
 Los datos que puede exportar se limitan a aquellos para los que tiene permiso de acceso. El permiso de acceso a datos se establece en la aplicación web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] o mediante programación.  
  
 Cuando exporte grandes cantidades de datos, puede establecer las advertencias que se mostrarán si los datos pueden tardar mucho en cargarse. Para ello, en el grupo **Opciones** , haga clic en **Configuración**. En la pestaña **Datos** , seleccione **Mostrar advertencia de filtro para grandes conjuntos de datos**.  
  
> [!WARNING]  
>  Es preciso abrir un libro habilitado para MDS y actualizarlo solo en Excel con un complemento de MDS para Excel. Cuando se abre un libro habilitado para MDS en Excel en un equipo en el que no esté instalado el complemento de MDS para Excel, o no se admita, podría dañarse el archivo del libro. Si desea compartir datos con otra persona, envíele por correo electrónico un archivo de consulta de acceso directo, en lugar de guardar la hoja de cálculo y enviarla por correo electrónico. Para obtener más información sobre la consulta, consulte [Enviar por correo electrónico un archivo de consulta de acceso directo &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md).  
  
## <a name="filtering-data"></a>Filtrado de datos  
 Puede filtrar los datos antes de exportarlos para limitar la cantidad de datos que se van a descargar. Esto incluye elegir qué atributos (columnas) desea cargar, el orden que desea mostrar los atributos y los miembros (filas de datos) con los que desea trabajar. Para más información, consulte [Filtrar los datos antes de exportar &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md).  
  
## <a name="connect-automatically-and-load-frequently-used-data"></a>Conectar automáticamente y cargar datos utilizados con frecuencia  
 Si quiere conectarse al mismo servidor y exportar siempre el mismo conjunto de datos, puede crear archivos de consulta de acceso directo, que contienen la información de conexión y filtro. Para obtener más información sobre los archivos de consulta, consulte [Archivos de consulta de acceso directo &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md).  
  
## <a name="refreshing-data"></a>Actualizar datos  
 Otros usuarios pueden actualizar los datos del repositorio MDS después de que usted los haya exportado. Puede recuperar estos datos sin perder los cambios realizados en los datos que no son de MDS. Para obtener más información, consulte [Actualizar datos &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Filtrar los datos MDS antes de cargarlos en Excel.|[Filtrar los datos antes de exportar &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)|  
|Cargar datos MDS en Excel.|[Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|Cambiar el orden de las columnas antes de descargar datos.|[Reordenar columnas &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Conexiones &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [Archivos de consulta de acceso directo &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Complemento Master Data Services para Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
-   [Seguridad &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  
