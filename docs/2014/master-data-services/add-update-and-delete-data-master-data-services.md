---
title: Agregar, actualizar y eliminar datos (Master Data Services) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2014
ms.assetid: b6295ead-bd2f-49dd-8756-35c6afb59648
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 665925f4d9298b3bfaf1dcc5841b78993978a94e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109261"
---
# <a name="add-update-and-delete-data-master-data-services"></a>Agregar, actualizar y eliminar datos (Master Data Services)
  Puede agregar datos y realizar cambios en los datos en un modelo de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], de forma masiva.  
  
 **Requisitos previos**  
  
-   Debe tener permiso para insertar datos en las tablas stg.\<nombre>_Leaf, stg.\<nombre>_Consolidated y stg.\<nombre>_Relationship de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
-   Debe tener permisos para ejecutar el procedimiento almacenado stg.udp_\<nombre>_Leaf, stg.udp\_\<nombre>_Consolidated o stg.udp\_\<nombre>_Relationship en la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
-   El modelo no debe tener un estado de **Confirmado**.  
  
 **Para agregar, actualizar y eliminar datos en la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]**  
  
1.  Prepare los miembros para importarlos en la tabla de almacenamiento provisional apropiada de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] y proporcione valores para los campos obligatorios. Para obtener información general de las tablas de almacenamiento provisional, consulte [importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
    -   Para los miembros hoja, la tabla es stg.\<nombre>_Leaf, donde \<nombre> hace referencia a la entidad correspondiente. Para obtener información sobre los campos obligatorios, consulte [Tabla de almacenamiento provisional de miembros hoja &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md)  
  
    -   Para los miembros consolidados, la tabla es stg.\<nombre>_Consolidated. Para obtener información sobre los campos obligatorios, consulte [Tabla de almacenamiento provisional de miembros consolidados &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md).  
  
    -   Para mover la ubicación de los miembros de jerarquías explícitas, la tabla es stg.\<nombre>_Relationship. Para obtener información sobre los campos obligatorios, consulte [Tabla de almacenamiento provisional de relaciones &#40;Master Data Services&#41;](../../2014/master-data-services/relationship-staging-table-master-data-services.md).  
  
         Para obtener información general acerca de cómo mover los miembros de jerarquías explícitas, vea [importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
    -   Use el valor del campo **ImportType** para especificar que está creando nuevos miembros, desactivando o eliminando miembros. Para obtener más información sobre los valores, consulte [Tabla de almacenamiento provisional de miembros hoja &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-member-staging-table-master-data-services.md) y [Tabla de almacenamiento provisional de miembros consolidados &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-member-staging-table-master-data-services.md).  
  
         Para obtener información general de la desactivación y eliminación de miembros, vea [importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
2.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de Motor de base de datos de su base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
     Para obtener más información, vea [SQL Server Management Studio](../ssms/sql-server-management-studio-ssms.md).  
  
3.  Importe datos en las tablas de almacenamiento provisional mediante el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Asistente para la importación y exportación.  
  
     Para obtener más información, vea [SQL Server Import and Export Wizard](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).  
  
4.  Lleve a cabo una de las siguientes operaciones para cargar los datos de las tablas de almacenamiento provisional en las tablas [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
    -   Ejecute el procedimiento almacenado de almacenamiento provisional que corresponde a la tabla de almacenamiento provisional a la que desea mover los datos.  
  
         Para obtener información general de los procedimientos almacenados de almacenamiento provisional y tablas de almacenamiento provisional, consulte [importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md). Para obtener más información sobre los parámetros de procedimientos almacenados de almacenamiento provisional y un ejemplo de código, consulte [Procedimiento almacenado de almacenamiento provisional &#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md).  
  
    -   Use el área funcional de **Administración de integraciones** de Administración de datos maestros.  
  
         En la página **Lotes de almacenamiento provisional** , seleccione el modelo al que va a agregar datos en la lista desplegable y, después, haga clic en **Iniciar lotes**. El estado del procesamiento por lotes se indica en el campo **Estado** . Para obtener más información sobre los estados, consulte [Estados de importación &#40;Master Data Services&#41;](../../2014/master-data-services/import-statuses-master-data-services.md).  
  
         ![Página Lotes de almacenamiento provisional en Master Data Manager](../../2014/master-data-services/media/mds-staging-batches.png "Página Lotes de almacenamiento provisional en Master Data Manager")  
  
         El proceso de almacenamiento provisional se inicia a intervalos definidos por el valor **Intervalo de lote de almacenamiento provisional** de [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../../2014/master-data-services/system-settings-master-data-services.md).  
  
5.  Vea los errores que se produjeron durante el almacenamiento provisional. Para obtener más información, consulte [ver los errores que se producen durante el proceso de almacenamiento provisional &#40;Master Data Services&#41; ](view-errors-that-occur-during-staging-master-data-services.md) y [errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](../../2014/master-data-services/staging-process-errors-master-data-services.md).  
  
6.  Valide los datos según reglas de negocios.  
  
     En Master Data Manager, navegue hasta el área funcional **Explorador** correspondiente a su modelo y, a continuación, aplique reglas de negocios para validar los datos. Para obtener más información, consulte [Validar miembros específicos con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md). También puede usar un procedimiento almacenado para validar los datos. Para obtener más información, consulte [Procedimiento almacenado de validación &#40;Master Data Services&#41;](../../2014/master-data-services/validation-stored-procedure-master-data-services.md).  
  
     Al cargar datos usando tablas de almacenamiento provisional, los datos no se validan automáticamente con las reglas de negocios. Para obtener más información sobre qué es la validación y cuándo ocurre, consulte [Validación &#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)  
  
  