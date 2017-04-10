---
title: "Especificar la ubicaci&#243;n predeterminada de instant&#225;neas (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantáneas [replicación de SQL Server], ubicaciones predeterminadas"
  - "ubicaciones predeterminadas de instantáneas"
ms.assetid: 27c5d9ad-a915-4c59-a8b7-82e3af61ac4d
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Especificar la ubicaci&#243;n predeterminada de instant&#225;neas (SQL Server Management Studio)
  Especifique la ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para configurar la distribución. Para obtener más información acerca de cómo utilizar este asistente, consulte [Configurar publicación y distribución](../../relational-databases/replication/configure-publishing-and-distribution.md). Si crea una publicación en un servidor que no está configurado como un distribuidor, especifique una ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para nueva publicación. Para obtener más información acerca de cómo utilizar este asistente, consulte [crear una publicación](../../relational-databases/replication/publish/create-a-publication.md).  
  
 Modificar la ubicación predeterminada de instantáneas en el **publicadores** página de la **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo. Para obtener más información, consulte [Propiedades de publicador y distribuidor modificar y vista](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md). Establecer la carpeta de instantáneas para cada publicación en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para más información, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### Para modificar la ubicación predeterminada de instantáneas  
  
1.  En el **publicadores** página de la **Propiedades del distribuidor: \< distribuidor>** diálogo cuadro, haga clic en el botón de propiedades (**...**) para el publicador para la que desea cambiar la ubicación predeterminada de instantáneas.  
  
2.  En la **Propiedades del publicador: \< publicador>** cuadro de diálogo, escriba un valor para el **carpeta de instantáneas predeterminada** propiedad.  
  
    > [!NOTE]  
    >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como una ruta de nomenclatura universal (UNC) de la convención, como \\\computername\snapshot. Para obtener más información, consulte [proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Vea también  
 [Ubicaciones alternativas para las carpetas de instantáneas](../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  