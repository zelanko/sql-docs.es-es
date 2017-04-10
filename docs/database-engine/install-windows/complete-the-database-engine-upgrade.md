---
title: "Completar la actualizaci&#243;n motor de base de datos | Microsoft Docs"
ms.custom: ""
ms.date: "09/22/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f08087e-e532-416c-8caa-e0ec88c57596
caps.latest.revision: 10
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 10
---
# Completar la actualizaci&#243;n motor de base de datos
  Una vez completada la actualización a SQL Server 2016, hay una serie de pasos adicionales que debe tomar. Entre ellas, figuran:  
  
 Después de actualizar el [!INCLUDE[ssDE](../../includes/ssde-md.md)], complete las siguientes tareas:  
  
-   **Realice una copia de seguridad de las bases de datos:** realice una copia de seguridad completa de cada base de datos actualizada.  
  
-   **Habilite nuevas características:** en SQL Server 2016, algunos cambios solo se habilitan una vez que se ha cambiado a 130 el nivel de DATABASE_COMPATIBILITY de una base de datos.  Para obtener más información y para ver el flujo de trabajo recomendado, vea [Cambiar el modo de compatibilidad de la base de datos y usar el almacén de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md).  
  
-   **Integration Services:**  
  
     Migre los paquetes de Integration Services al formato [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, consulte [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
-   **Reporting Services:** para una nueva actualización de instalación, restaure las claves de cifrado de Reporting Services. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/back-up-and-restore-reporting-services-encryption-keys.md).  
  
-   **Master Data Services:** actualice el esquema de base de datos MDS y cree la aplicación web de SQL Server 2016. Para obtener más información, vea [Actualizar Master Data Services](../../database-engine/install-windows/upgrade-master-data-services.md).  
  
-   **Data Quality Services:** actualice el esquema de base de datos DQS y compruebe la actualización del esquema de base de datos DQS. Para obtener más información, vea [Actualizar Data Quality Services](../../database-engine/install-windows/upgrade-data-quality-services.md).  
  
-   **Búsqueda de texto completo:** vuelva a rellenar los catálogos de texto completo para garantizar la coherencia semántica de los resultados de las consultas. Para obtener más información, vea [Rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
## ¿Le ayudó este artículo? Le escuchamos  
 ¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Complete%20the%20Database%20Engine%20Upgrade%20page)  
  
  