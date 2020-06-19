---
title: Complemento Master Data Services para Microsoft Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f84048371eac930974ebbd3d0693e25761f9a784
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961165"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Complemento Master Data Services para Microsoft Excel
  Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] , las listas maestras de datos de referencia se pueden distribuir a todos los usuarios de la organización que usen Excel. La seguridad determina los datos que los usuarios pueden ver y actualizar.  
  
 Puede cargar listas filtradas de datos MDS en Excel, donde puede trabajar con ellos al igual que otros datos cualesquiera. Cuando termine, puede publicar los datos en MDS, donde se almacenan centralmente.  
  
 Si es administrador, use [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] para crear entidades y atributos, y cargarlos con datos. Esto elimina la necesidad de utilizar cualquier otra herramienta para cargar datos en los modelos.  
  
 En [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], puede usar Data Quality Services (DQS) para comparar los datos antes de cargarlos en MDS. Esto ayuda a evitar datos duplicados en MDS.  
  
> [!IMPORTANT]  
>  Puede continuar con la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 de servicios del complemento Master Data Services para Excel después de actualizar Master Data Services y Data Quality Services a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Sin embargo, las versiones anteriores del complemento de Master Data Services para Excel no funcionarán después de actualizar a SQL Server 2014 CTP2. Puede descargar la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 del complemento de Master Data Services para Excel [aquí](https://go.microsoft.com/fwlink/?LinkId=328664).  
  
## <a name="terms"></a>Términos  
 Al trabajar con el complemento, puede encontrar los siguientes términos.  
  
-   El *MDS repository* es donde se almacenan todos los datos maestros. Es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada para almacenar datos de MDS. Para trabajar con datos del repositorio, los datos se cargan en Excel; cuando haya terminado, puede volver a publicar los cambios en el repositorio. Los administradores pueden agregar nuevas entidades y atributos al repositorio.  
  
-   Los*datos administrados con MDS* son aquellos datos que se almacenan en el repositorio MDS y se cargan en Excel, donde se muestran como filas resaltadas. Puede agregar datos no administrados por MDS a una hoja de cálculo, y esto no les afecta al actualizar los datos administrados por MDS.  
  
-   Un *model* es un contenedor de datos. Se pueden crear versiones de estos contenedores y normalmente la última versión es la más reciente. Para obtener más información, consulte [Modelos &#40;Master Data Services&#41;](../models-master-data-services.md).  
  
-   Una *entity* es una lista de datos. Puede que piense en una entidad como una tabla en una base de datos. Por ejemplo, la entidad **Color** puede contener una lista de colores. Para obtener más información, consulte [Entidades &#40;Master Data Services&#41;](../entities-master-data-services.md).  
  
-   Un *member* es una fila de datos. Cada entidad contiene miembros. Un ejemplo de un miembro es **Azul**. Para obtener más información, consulte [Miembros &#40;Master Data Services&#41;](../members-master-data-services.md).  
  
-   Un *attribute* es una columna de datos. Cada miembro tiene atributos. Por ejemplo, el atributo **code** del miembro **Blue** es **B**. Para obtener más información sobre los atributos, vea [atributos &#40;Master Data Services&#41;](../attributes-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear una conexión a un repositorio de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Conectarse a un repositorio MDS &#40;complemento MDS para Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Cargar los datos administrados por MDS en Excel.|[Cargar datos de MDS en Excel](export-data-to-excel-from-master-data-services.md)|  
|Guardar una consulta de acceso directo que se puede usar para abrir en el futuro los datos mostrados, administrados por MDS actualmente.|[Guardar un archivo de consulta de acceso directo &#40;complemento MDS para Excel&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Compartir los métodos abreviados con otros.|[Enviar por correo electrónico un archivo de consulta de acceso directo &#40;complemento MDS para Excel&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Ver todos los cambios realizados en un miembro.|[Ver todas las anotaciones o transacciones de un miembro &#40;complemento MDS para Excel&#41;](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Antes de publicar nuevos datos, averigüe si existe la replicación.|[Coincidir datos similares &#40;Complemento MDS para Excel&#41;](match-similar-data-mds-add-in-for-excel.md)|  
|Publicar datos de una hoja de cálculo en el repositorio MDS.|[Publicar datos de Excel en MDS &#40;Complemento MDS para Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Crear una nueva entidad con datos de la hoja de cálculo. (Solo administradores)|[Crear una entidad &#40;Complemento MDS para Excel&#41;](create-an-entity-mds-add-in-for-excel.md)|  
|Crear un atributo basado en dominio, también conocido como lista restringida. (Solo administradores)|[Crear un atributo basado en dominio &#40;complemento MDS para Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Establezca las propiedades para cargar y publicar datos del complemente Master Data Services para Excel. (Solo administradores)|[Establecer propiedades para el complemento Master Data Services para Excel](setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Conexiones &#40;complemento MDS para Excel&#41;](connections-mds-add-in-for-excel.md)  
  
-   [Cargando datos &#40;Complemento MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Archivos de consulta de acceso directo &#40;complemento MDS para Excel&#41;](shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Coincidencia de calidad de datos en el Complemento MDS para Excel](data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [Complemento MDS para Excel de &#40;de datos de publicación&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Generar un modelo &#40;complemento MDS para Excel&#41;](building-a-model-mds-add-in-for-excel.md)  
  
-   [Seguridad &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  
