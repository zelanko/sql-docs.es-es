---
title: Modificación de las opciones de inicialización de instantáneas para la replicación de SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshot replication [SQL Server], options
- snapshots [SQL Server replication], options
ms.assetid: 759fab42-66c7-4541-a7a3-bb6fb868493c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a611de458537156740521dae8b732eed3e2653c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270260"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>Modificación de las opciones de inicialización de instantáneas para la replicación de SQL

Este artículo describe cómo modificar una serie de opciones cuando [inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md).

## <a name="snapshot-format"></a>Formato de instantánea
  Especifique el formato de instantánea en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  

1.  En la página **Instantánea**, del cuadro de diálogo **Propiedades de la publicación: \<publicación>** , seleccione **SQL Server nativo: todos los suscriptores deben ser servidores que ejecuten SQL Server** o **Carácter: es necesario si un publicador o suscriptor no ejecuta SQL Server**. 

    > [!NOTE]  
    >  Se recomienda seleccionar el formato nativo, a menos que esta publicación deba ser compatible con suscripciones a una base de datos de [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o una base de datos que no sea de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="snapshot-folder-locations"></a>Ubicaciones de carpeta de instantáneas

### <a name="default-snapshot-location"></a>Ubicación predeterminada de instantáneas
Especifique la ubicación predeterminada de instantáneas (SQL Server Management Studio) de forma predeterminada la ubicación de la instantánea en la **carpeta de instantáneas** página del Asistente para configurar la distribución. Para obtener más información sobre cómo usar este asistente, vea [Configure Publishing and Distribution](configure-publishing-and-distribution.md) (Configurar la publicación y la distribución). Si crea una publicación en un servidor que no está configurado como un distribuidor, especifique una ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para nueva publicación. Para obtener más información sobre cómo usar este asistente, vea [Create a Publication](publish/create-a-publication.md) (Crear una publicación).  
  
 Modifique la ubicación de instantáneas predeterminada en la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor \<distribuidor>** . Para obtener más información, vea [View and Modify Distributor and Publisher Properties](view-and-modify-distributor-and-publisher-properties.md) (Ver y modificar las propiedades del distribuidor y del publicador). Establezca la carpeta de instantáneas para cada publicación en el cuadro de diálogo **Propiedades de la publicación - \<publicación>** . Para más información, consulte [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
#### <a name="modify-the-default-snapshot-location"></a>Modificación de la ubicación predeterminada de instantáneas  
  
1.  En la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>** , haga clic en el botón de propiedades ( **...** ) correspondiente al publicador para el que quiera cambiar la ubicación de instantáneas predeterminada.    
2.  En el cuadro de diálogo **Propiedades del publicador - \<publicador>** , escriba un valor para la propiedad **Carpeta de instantáneas predeterminada**.

    > [!NOTE]  
    >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para obtener más información, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md).    
1.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

### <a name="alternate-snapshot-location"></a>Ubicación de instantáneas alternativa
  Especifique una ubicación de instantáneas alternativa en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md). 

  
#### <a name="specify-an-alternate-snapshot-location"></a>Especificar una ubicación de instantáneas alternativa  
  
1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** :    
    1.  Seleccione **Poner los archivos en la siguiente carpeta**y haga clic en **Examinar** para navegar al directorio, o bien escriba la ruta de acceso al directorio en el que deben almacenarse los archivos de instantáneas.    

        > [!NOTE]  
        >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para obtener más información, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md).    
    a.  Desactive la casilla **Poner los archivos en la carpeta predeterminada** , a menos que necesite copiar los archivos de instantáneas en ambas ubicaciones.    
     Para comprimir los archivos de instantáneas, seleccione **Comprimir archivos de instantánea en esta carpeta**. La compresión se utiliza generalmente para las conexiones con poco ancho de banda y las ubicaciones de instantánea alternativas en medios extraíbles, como un CD-ROM.    
1.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]   


## <a name="compress-snapshot-files"></a>Comprimir archivos de instantáneas
Especifique que se deben comprimir los archivos en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** :  
  
    1.  Seleccione **Poner los archivos en la siguiente carpeta**y haga clic en **Examinar** para navegar al directorio, o bien escriba la ruta de acceso al directorio en el que deben almacenarse los archivos de instantáneas.    
        > [!NOTE]  
        >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para más información, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md).  
  
    2.  Desactive la casilla **Poner los archivos en la carpeta predeterminada** , a menos que necesite copiar los archivos de instantáneas en ambas ubicaciones.    
        > [!NOTE]  
        >  Si esta casilla está activada, los archivos almacenados en la carpeta predeterminada no se comprimen. Los archivos comprimidos solo se pueden almacenar en la ubicación alternativa especificada en el paso anterior.    
2.  Active **Comprimir archivos de instantánea en esta carpeta**.    
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>Ejecución de scripts antes y después de aplicar una instantánea

 Puede especificar scripts que se ejecuten en el suscriptor antes o después de aplicar la instantánea. Los scripts pueden utilizarse por distintos motivos, por ejemplo, para crear inicios de sesión y esquemas (propietarios de objetos) en cada suscriptor.  
  
 Al especificar una ubicación de archivos para cada script, el Agente de instantáneas copia los archivos de script en la carpeta actual de instantáneas cada vez que se procesan instantáneas. El Agente de distribución o el Agente de mezcla ejecutan el script previo a la instantánea antes que cualquiera de los scripts de objetos replicados al aplicar una instantánea. El Agente de distribución o el Agente de mezcla ejecutan el script posterior a la instantánea después de aplicar todos los demás datos y scripts de objetos replicados. Después de completar la aplicación de instantáneas y de ejecutar correctamente los archivos de script, estos archivos se quitan del directorio de trabajo del suscriptor.  
  
 El script se ejecuta con la utilidad **sqlcmd** . Antes de implementar un script, ejecútelo con **sqlcmd** para asegurarse de que se ejecuta según lo previsto. El contenido de los scripts que se ejecutan antes y después de aplicar la instantánea debe ser repetible. Por ejemplo, si crea una tabla en el script, debe comprobar primero si ya existe y tomar las medidas apropiadas si no existe. El script debe ser repetible, porque si necesita reinicializar una suscripción en la que ya se aplicó el script, este se volverá a aplicar cuando se aplique la nueva instantánea durante la reinicialización.  
  
 Si comprime el archivo de instantáneas en formato CAB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , los scripts también se comprimen y se colocan en el archivo CAB. Después de que el archivo de instantáneas comprimido se transfiere al suscriptor y se descomprime en un directorio de trabajo del suscriptor, se ejecutan los scripts indicados como anteriores a la instantánea. De la misma manera, los scripts posteriores a la instantánea se descomprimen y se ejecutan en el suscriptor como el último paso para la aplicación de la instantánea.  

### <a name="execute-a-script-before-or-after-a-snapshot-is-applied"></a>Ejecute una secuencia de comandos antes o después de aplicar una instantánea  
 Especifique un script opcional para que se ejecute antes o después de aplicar la instantánea en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  


1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** :    
    -   Para especificar un script para que se ejecute antes de aplicar la instantánea, haga clic en **Examinar** para navegar al script, o escriba la ruta de acceso del script en el cuadro de texto **Antes de aplicar la instantánea, ejecutar este script** . 
   
        > [!NOTE]  
        >  El Agente de distribución o el Agente de mezcla debe tener permisos de lectura para el directorio especificado. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso de convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\scripts\myscript.sql.    
    -   Para especificar un script para que se ejecute después de aplicar la instantánea, haga clic en **Examinar** para navegar al script, o escriba la ruta de acceso UNC al script en el cuadro de texto **Después de aplicar la instantánea, ejecutar este script** .    
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  
  
