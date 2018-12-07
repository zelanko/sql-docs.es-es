---
title: Complemento Master Data Services para Microsoft Excel | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 5b9e328f3abd3a53bfb4764470138d6d6b966236
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617605"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Complemento Master Data Services para Microsoft Excel

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], puede cargar listas filtradas de datos de MDS a Excel y trabajar con ellas igual que con cualquier dato. Cuando termine, puede publicar los datos en MDS, donde se almacenan centralmente. La seguridad determina los datos que los usuarios pueden ver y actualizar.  
  
 Si es administrador, use [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] para crear entidades y atributos, y cargarlos con datos. Esto elimina la necesidad de utilizar cualquier otra herramienta para cargar datos en los modelos.  
  
 En [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], puede usar Data Quality Services (DQS) para comparar los datos antes de cargarlos en MDS. Esto ayuda a evitar datos duplicados en MDS.  

## <a name="downloads"></a>Descargas 
>*  Descargue el complemento de Master Data Services para Excel para SQL Server 2016 SP2 en [esta página del Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=56838). 
>* Descargue [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] para SQL Server 2017 en [esta página del Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=836867).
 
  
## <a name="terms"></a>Términos  
 Al trabajar con el complemento, puede encontrar los siguientes términos. Para obtener más información sobre estos conceptos, consulte [Introducción a Master Data Services &#40;MDS&#41;](../../master-data-services/master-data-services-overview-mds.md).  
  
-   El *MDS repository* es donde se almacenan todos los datos maestros. Es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada para almacenar datos de MDS. Para trabajar con datos del repositorio, los datos se cargan en Excel; cuando haya terminado, puede volver a publicar los cambios en el repositorio. Los administradores pueden agregar nuevas entidades y atributos al repositorio.  
  
-   Los*datos administrados con MDS* son aquellos datos que se almacenan en el repositorio MDS y se cargan en Excel, donde se muestran como filas resaltadas. Puede agregar datos no administrados por MDS a una hoja de cálculo, y esto no les afecta al actualizar los datos administrados por MDS.  
  
-   Un *model* es un contenedor de datos. Se pueden crear versiones de estos contenedores y normalmente la última versión es la más reciente. Para obtener más información, consulte [Modelos &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md).  
  
-   Una *entity* es una lista de datos. Puede que piense en una entidad como una tabla en una base de datos. Por ejemplo, la entidad **Color** puede contener una lista de colores. Para obtener más información, consulte [Entidades &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md).  
  
-   Un *miembro* es una fila de datos (un registro). Cada entidad contiene miembros. Un ejemplo de un miembro es **Azul**. Para obtener más información, consulte [Miembros &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md).  
  
-   Un *attribute* es una columna de datos. Cada miembro tiene atributos. Por ejemplo, el atributo **Código** del miembro **Azul** es **A**. Para obtener más información sobre los atributos, consulte [Atributos &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear una conexión a un repositorio de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Conectarse a un repositorio MDS &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Cargar los datos administrados por MDS en Excel.|[Exportar datos a Excel desde Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|Guardar una consulta de acceso directo que se puede usar para abrir en el futuro los datos mostrados, administrados por MDS actualmente.|[Guardar un archivo de consulta de acceso directo &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Compartir los métodos abreviados con otros.|[Enviar por correo electrónico un archivo de consulta de acceso directo &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Ver todos los cambios realizados en un miembro.|[Ver todas las anotaciones o transacciones de un miembro &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Antes de publicar nuevos datos, averigüe si existe la replicación.|[Coincidir datos similares &#40;Complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
|Publicar datos de una hoja de cálculo en el repositorio MDS.|[Importar datos de Excel en Master Data Services &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Crear una nueva entidad con datos de la hoja de cálculo. (Solo administradores)|[Crear una entidad &#40;Complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|Crear un atributo basado en dominio, también conocido como lista restringida. (Solo administradores)|[Crear un atributo basado en dominio &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Establezca las propiedades para cargar y publicar datos del complemente Master Data Services para Excel. (Solo administradores)|[Establecer propiedades para el complemento Master Data Services para Excel](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Conexiones &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [Información general: Exportar datos a Excel &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Archivos de consulta de acceso directo &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Actualizar datos &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Información general: Importación de datos desde Excel &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Validar datos &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
-   [Coincidencia de calidad de datos en el Complemento MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [Generar un modelo &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
-   [Establecer propiedades para el complemento Master Data Services para Excel](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)  
  
-   [Seguridad &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  
