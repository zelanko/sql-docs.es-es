---
title: Modificación de las opciones de inicialización de instantáneas para la replicación de SQL | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 68e61f26cc33d505ec183e3d863cfa3a6f407275
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586431"
---
# <a name="modify-snapshot-initialization-options-for-sql-replication"></a>Modificación de las opciones de inicialización de instantáneas para la replicación de SQL 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Hay varias opciones disponibles que se pueden especificar al [inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md).

## <a name="specify-snapshot-format-sql-server-management-studio"></a>Especificar el formato de instantánea (SQL Server Management Studio)
  Especifique el formato de instantánea en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<publicación>** . Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Para especificar el formato de instantánea  
  
1.  En la página **Instantánea**, del cuadro de diálogo **Propiedades de la publicación: \<publicación>** , seleccione **SQL Server nativo: todos los suscriptores deben ser servidores que ejecuten SQL Server** o **Carácter: es necesario si un publicador o suscriptor no ejecuta SQL Server**.  
  
    > [!NOTE]  
    >  Se recomienda seleccionar el formato nativo, a menos que esta publicación deba ser compatible con suscripciones a una base de datos de SQL Server Compact o una base de datos que no sea de SQL Server.  
  
2.  Seleccione **Aceptar**.   

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="snapshot-folder-locations"></a>Ubicaciones para las carpetas de instantáneas

### <a name="default-snapshot-location"></a>Ubicación predeterminada de instantáneas
Especifique la ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para configurar la distribución. Para obtener más información sobre cómo usar este asistente, vea [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md) (Configurar la publicación y la distribución). Si crea una publicación en un servidor que no está configurado como un distribuidor, especifique una ubicación predeterminada de instantáneas en la página **Carpeta de instantáneas** del Asistente para nueva publicación. Para obtener más información sobre cómo usar este asistente, vea [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md) (Crear una publicación).  
  
 Modifique la ubicación de instantáneas predeterminada en la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor \<distribuidor>** . Para obtener más información, vea [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md) (Ver y modificar las propiedades del distribuidor y del publicador). Establezca la carpeta de instantáneas para cada publicación en el cuadro de diálogo **Propiedades de la publicación - \<publicación>** . Para más información, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-modify-the-default-snapshot-location"></a>Para modificar la ubicación predeterminada de instantáneas  
  
1.  En la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>** , haga clic en el botón de propiedades ( **?** ) correspondiente al publicador para el que quiera cambiar la ubicación de instantáneas predeterminada.    
2.  En el cuadro de diálogo **Propiedades del publicador - \<publicador>** , escriba un valor para la propiedad **Carpeta de instantáneas predeterminada**.  
  
    > [!NOTE]  
    >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para obtener más información, vea [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).    
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
 

### <a name="alternate-snapshot-locations"></a>Ubicaciones alternativas de instantáneas
Las ubicaciones alternativas para las instantáneas permiten almacenar archivos de instantáneas en una ubicación distinta de la predeterminada o en otra ubicación además de la predeterminada, que suele encontrarse en el distribuidor. Las ubicaciones alternativas pueden encontrarse en otro servidor, en una unidad de red o en medios extraíbles, como discos CD-ROM o discos extraíbles.  
  
Las ubicaciones alternativas de las instantáneas se almacenan como una propiedad de la publicación. Debido a que la ubicación alternativa de la instantánea es una propiedad de la publicación, el Agente de distribución y el de mezcla pueden localizar la instantánea adecuada como parte del proceso de sincronización.  
  
Si desea especificar una ubicación diferente para la carpeta de instantáneas o si desea comprimir los archivos de instantáneas, cree la publicación sin crear la instantánea inicial inmediatamente, defina las propiedades de la publicación para la ubicación de la instantánea y ejecute el Agente de instantáneas para dicha publicación. Si cambia la ubicación alternativa después de crear la instantánea inicial, la ubicación de una instantánea generada para la publicación no se reubicará en la nueva ubicación alternativa. En este caso, dependiendo de la configuración de la publicación, es posible que el Agente de mezcla o el Agente de distribución encuentren los archivos de instantáneas en la nueva ubicación alternativa.  
  
> [!NOTE]  
>  No especifique una ubicación alternativa (con el cuadro de diálogo **Propiedades de la publicación** o [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)), que sea la misma que la ubicación de la carpeta predeterminada de instantáneas.  
  
> [!CAUTION]  
>  No use WebSync y las ubicaciones alternativas de carpeta de instantáneas a la vez.  
  
#### <a name="use-sql-server-management-studio"></a>Usar SQL Server Management Studio
1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** :  
  
    1.  Seleccione **Poner los archivos en la siguiente carpeta**y haga clic en **Examinar** para navegar al directorio, o bien escriba la ruta de acceso al directorio en el que deben almacenarse los archivos de instantáneas.  
  
        > [!NOTE]  
        >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si usa suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para obtener más información, vea [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
    2.  Desactive la casilla **Poner los archivos en la carpeta predeterminada** , a menos que necesite copiar los archivos de instantáneas en ambas ubicaciones.  
  
     Para comprimir los archivos de instantáneas, seleccione **Comprimir archivos de instantánea en esta carpeta**. La compresión se utiliza generalmente para las conexiones con poco ancho de banda y las ubicaciones de instantánea alternativas en medios extraíbles, como un CD-ROM.  
  
2.  Seleccione **Aceptar**.  
  
#### <a name="use-transact-sql"></a>Uso de Transact-SQL 

Cuando [configure propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md), especifique el valor de **snapshot_in_defaultfolder** como false. 

## <a name="compressed-snapshots"></a>Instantáneas comprimidas
  La compresión de los archivos de instantáneas es apropiada para transferir instantáneas a través de una red lenta o para guardarlas en un soporte extraíble, cuando la instantánea sin comprimir es demasiado grande. La compresión de los archivos de instantáneas resulta útil en estos casos, pero aumenta el tiempo necesario para generar y aplicar la instantánea.  
  
 Los archivos de instantáneas comprimidos se escriben en formato de archivo CAB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , que permite comprimir archivos de hasta 2 GB (si el archivo de instantánea tiene más de 2 GB, no se puede comprimir). Para comprimir archivos, es necesario copiarlos a otra carpeta de instantáneas (los archivos de la carpeta de instantáneas predeterminada no se pueden comprimir). 
  
 Los archivos se descomprimen en la ubicación en la que se ejecuta el Agente de distribución o de mezcla; por lo general, se usan suscripciones de extracción con las instantáneas comprimidas para descomprimir los archivos en el suscriptor. Cuando el suscriptor recibe un archivo comprimido, lo copia inicialmente a una ubicación temporal. Una vez copiado el archivo comprimido en el suscriptor, la utilidad CAB descomprime los archivos de instantáneas de uno en uno, en orden. El espacio necesario en el suscriptor es el tamaño del archivo comprimido más el del archivo más grande sin comprimir.  
  
> [!NOTE]  
>  En algunos casos, las instantáneas comprimidas pueden mejorar el rendimiento de la transferencia de archivos de instantáneas en la red. No obstante, la compresión de instantáneas requiere que el Agente de instantáneas realice un procesamiento adicional al generar los archivos de instantáneas, y otro procesamiento adicional por parte del Agente de distribución o del Agente de mezcla al aplicar los archivos de instantáneas. Esto puede ralentizar, en algunos casos, la generación de instantáneas y aumentar el tiempo de aplicación de una instantánea. Además, las instantáneas comprimidas no se pueden reanudar si se produce un error de red; por tanto, no son adecuadas para redes no confiables. Cuando utilice instantáneas comprimidas en una red, tenga en cuenta estos inconvenientes.  
  
### <a name="use-sql-server-management-studio"></a>Usar SQL Server Management Studio
1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** :  
  
    1.  Seleccione **Poner los archivos en la siguiente carpeta**y haga clic en **Examinar** para navegar al directorio, o bien escriba la ruta de acceso al directorio en el que deben almacenarse los archivos de instantáneas.  
  
        > [!NOTE]  
        >  El Agente de instantáneas debe tener permisos de escritura para el directorio especificado y el Agente de distribución o de mezcla debe tener permisos de lectura. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso, según la convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\instantánea. Para más información, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md).  
  
    2.  Desactive la casilla **Poner los archivos en la carpeta predeterminada** , a menos que necesite copiar los archivos de instantáneas en ambas ubicaciones.  
  
        > [!NOTE]  
        >  Si esta casilla está activada, los archivos almacenados en la carpeta predeterminada no se comprimen. Los archivos comprimidos solo se pueden almacenar en la ubicación alternativa especificada en el paso anterior.  
  
2.  Active **Comprimir archivos de instantánea en esta carpeta**.    
3.  Seleccione **Aceptar**.   

### <a name="use-transact-sql"></a>Uso de Transact-SQL

Cuando [configure propiedades de instantáneas](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md), especifique el valor **compress_snapshot** como **True**. 

## <a name="execute-scripts-before-and-after-snapshot-is-applied"></a>Ejecución de scripts antes y después de aplicar una instantánea
Puede especificar scripts que se ejecuten en el suscriptor antes o después de aplicar la instantánea. Los scripts pueden utilizarse por distintos motivos, por ejemplo, para crear inicios de sesión y esquemas (propietarios de objetos) en cada suscriptor.  
  
 Al especificar una ubicación de archivos para cada script, el Agente de instantáneas copia los archivos de script en la carpeta actual de instantáneas cada vez que se procesan instantáneas. El Agente de distribución o el Agente de mezcla ejecutan el script previo a la instantánea antes que cualquiera de los scripts de objetos replicados al aplicar una instantánea. El Agente de distribución o el Agente de mezcla ejecutan el script posterior a la instantánea después de aplicar todos los demás datos y scripts de objetos replicados. Después de completar la aplicación de instantáneas y de ejecutar correctamente los archivos de script, estos archivos se quitan del directorio de trabajo del suscriptor.  
  
 El script se ejecuta con la utilidad **sqlcmd** . Antes de implementar un script, ejecútelo con **sqlcmd** para asegurarse de que se ejecuta según lo previsto. El contenido de los scripts que se ejecutan antes y después de aplicar la instantánea debe ser repetible. Por ejemplo, si crea una tabla en el script, debe comprobar primero si ya existe y tomar las medidas apropiadas si no existe. El script debe ser repetible, porque si necesita reinicializar una suscripción en la que ya se aplicó el script, este se volverá a aplicar cuando se aplique la nueva instantánea durante la reinicialización.  
  
 Si comprime el archivo de instantáneas en formato CAB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , los scripts también se comprimen y se colocan en el archivo CAB. Después de que el archivo de instantáneas comprimido se transfiere al suscriptor y se descomprime en un directorio de trabajo del suscriptor, se ejecutan los scripts indicados como anteriores a la instantánea. De la misma manera, los scripts posteriores a la instantánea se descomprimen y se ejecutan en el suscriptor como el último paso para la aplicación de la instantánea.  

### <a name="execute-a-script"></a>Ejecución de un script 

1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>** :    
    -   Para especificar un script para que se ejecute antes de aplicar la instantánea, haga clic en **Examinar** para navegar al script, o escriba la ruta de acceso del script en el cuadro de texto **Antes de aplicar la instantánea, ejecutar este script** .  
  
        > [!NOTE]  
        >  El Agente de distribución o el Agente de mezcla debe tener permisos de lectura para el directorio especificado. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso de convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\scripts\myscript.sql.  
  
    -   Para especificar un script para que se ejecute después de aplicar la instantánea, haga clic en **Examinar** para navegar al script, o escriba la ruta de acceso UNC al script en el cuadro de texto **Después de aplicar la instantánea, ejecutar este script** .   
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  


## <a name="see-also"></a>Consulte también  
 [Inicializar una suscripción con una instantánea](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Transferencia de una instantánea mediante FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)   
 [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)     
  
  
