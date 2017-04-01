---
title: "Importar datos de tablas (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad5b83b1-8e40-4ef8-9ba8-4ea17a58b672
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Importar datos de tablas (Master Data Services)
  Puede agregar datos y realizar cambios en los datos en un modelo de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], de forma masiva.  
  
 **Requisitos previos**  
  
-   Debe tener permiso para insertar datos en la tabla stg.\<nombre>_Leaf, stg.\<nombre>_Consolidated y stg.\<nombre>_Relationship de la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
-   Debe tener permisos para ejecutar el procedimiento almacenado stg.udp_\<nombre>_Leaf, stg.udp\_\<nombre>_Consolidated o stg.udp\_\<nombre>_Relationship en la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
-   El modelo no debe tener un estado de **Confirmado**.  
  
 **Para agregar, actualizar y eliminar datos en la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]**  
  
1.  Prepare los miembros para importarlos en la tabla de almacenamiento provisional apropiada de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] y proporcione valores para los campos obligatorios. Para obtener más información sobre las tablas de almacenamiento provisional, consulte [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
    -   Para los miembros hoja la tabla es stg.\<nombre>_Leaf, donde \<nombre> hace referencia a la entidad correspondiente. Para obtener información sobre los campos obligatorios, consulte [Tabla de almacenamiento provisional de miembros hoja &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md)  
  
    -   Para los miembros consolidados, la tabla es stg.\<nombre>_Consolidated. Para obtener información sobre los campos obligatorios, consulte [Tabla de almacenamiento provisional de miembros consolidados &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md).  
  
    -   Para mover la ubicación de los miembros de jerarquías explícitas, la tabla es stg.\<nombre>_Relationship. Para obtener información sobre los campos obligatorios, consulte [Tabla de almacenamiento provisional de relaciones &#40;Master Data Services&#41;](../master-data-services/relationship-staging-table-master-data-services.md).  
  
         Para obtener información general sobre cómo mover miembros en jerarquías explícitas, consulte [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
    -   Use el valor del campo **ImportType** para especificar que está creando nuevos miembros, desactivando o eliminando miembros. Para obtener más información sobre los valores, consulte [Tabla de almacenamiento provisional de miembros hoja &#40;Master Data Services&#41;](../master-data-services/leaf-member-staging-table-master-data-services.md) y [Tabla de almacenamiento provisional de miembros consolidados &#40;Master Data Services&#41;](../master-data-services/consolidated-member-staging-table-master-data-services.md).  
  
         Para obtener información general sobre cómo desactivar y eliminar miembros, consulte [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md).  
  
2.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de Motor de base de datos de su base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
     Para obtener más información, vea [SQL Server Management Studio](../Topic/SQL%20Server%20Management%20Studio.md).  
  
3.  Importe datos en las tablas de almacenamiento provisional mediante el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Asistente para la importación y exportación.  
  
     Para obtener más información, vea [SQL Server Import and Export Wizard](../Topic/SQL%20Server%20Import%20and%20Export%20Wizard.md).  
  
4.  Lleve a cabo una de las siguientes operaciones para cargar los datos de las tablas de almacenamiento provisional en las tablas [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
    -   Ejecute el procedimiento almacenado de almacenamiento provisional que corresponde a la tabla de almacenamiento provisional a la que desea mover los datos.  
  
         Para obtener información general sobre procedimientos almacenados de almacenamiento provisional y tablas de almacenamiento provisional, consulte [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md). Para obtener más información sobre los parámetros de procedimientos almacenados de almacenamiento provisional y un ejemplo de código, consulte [Procedimiento almacenado de almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md).  
  
    -   Use el área funcional de **Administración de integraciones** de Administración de datos maestros.  
  
         En la página **Lotes de almacenamiento provisional**, seleccione el modelo al que va a agregar datos en la lista desplegable y, después, haga clic en **Iniciar lotes**. El estado del procesamiento por lotes se indica en el campo **Estado** . Para obtener más información sobre los estados, consulte [Estados de importación &#40;Master Data Services&#41;](../master-data-services/import-statuses-master-data-services.md).  
  
         ![Staging Batches Page in Master Data Manager](../master-data-services/media/mds-stagingbatchespage.png "Staging Batches Page in Master Data Manager")  
  
         El proceso de almacenamiento provisional se inicia a intervalos definidos por el valor **Intervalo de lote de almacenamiento provisional** de [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
5.  Vea los errores que se produjeron durante el almacenamiento provisional. Para obtener más información, consulte [Ver los errores que se producen durante el almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md) y [Errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
6.  Valide los datos según reglas de negocios.  
  
     En Master Data Manager, navegue hasta el área funcional **Explorador** correspondiente a su modelo y, a continuación, aplique reglas de negocios para validar los datos. Para obtener más información, consulte [Validar miembros específicos con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md). También puede usar un procedimiento almacenado para validar los datos. Para obtener más información, consulte [Procedimiento almacenado de validación &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
     Al cargar datos usando tablas de almacenamiento provisional, los datos no se validan automáticamente con las reglas de negocios. Para obtener más información sobre qué es la validación y cuándo ocurre, consulte [Validación &#40;Master Data Services&#41;](../master-data-services/validation-master-data-services.md).  
  
  