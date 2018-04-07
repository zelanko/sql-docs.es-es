---
title: Hoja de cálculo de planeación de la capacidad de copia de seguridad de servidor (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Esta hoja de cálculo de planeación de capacidad le ayuda a determinar los requisitos para un servidor de copia de seguridad para realizar la copia de seguridad de base de datos de SQL Server PDW y las operaciones de restauración.
ms.date: 01/05/2017
ms.topic: article
ms.assetid: 36294bf6-6dde-481f-a190-d4382b04c030
caps.latest.revision: 6
ms.openlocfilehash: 1548d284f78043e5f878bafe9922480fe762dbfe
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="backup-server-capacity-planning-worksheet"></a>Hoja de planificación de capacidad de copia de seguridad de servidor
Esta hoja de cálculo de planeación de capacidad le ayuda a determinar los requisitos para un servidor de copia de seguridad para realizar la copia de seguridad de base de datos de SQL Server PDW y las operaciones de restauración. Utilícelo para crear un plan de compras nuevos o aprovisionamiento copia de seguridad servidores existentes.  
  
Esta hoja de cálculo es un complemento para las instrucciones de [adquirir y configurar un servidor de copia de seguridad](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Hoja de planificación de capacidad para los servidores de copia de seguridad  

### <a name="notes"></a>Notas  
  
1.  Esta hoja de cálculo se aplica a los servidores que se va a realizar las operaciones de copia de seguridad y restauración para bases de datos PDW.  
  
2.  La única forma de copia de seguridad y restaurar bases de datos PDW es usar los comandos de base de datos de copia de seguridad y restaurar bases de datos SQL. Sin embargo, una vez que los datos de copia de seguridad están en el servidor de copia de seguridad, existe como un conjunto de archivos de Windows. Para archivar los archivos de copia de seguridad desde el servidor a otra ubicación de almacenamiento mediante el uso de métodos copia de seguridad tradicionales de Windows basada en archivos.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Icono del Portapapeles](media/clipboard-icon.png "el icono del Portapapeles") hoja de cálculo de planeación de capacidad 
  
Imprimir esta hoja de cálculo y rellenarlo con sus propios requisitos.  
  
|Componente|Requisito|Rellene esta columna con sus propios requisitos|Recomendaciones|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Almacenamiento|Número máximo de bytes que vaya a almacenar en el servidor de copia de seguridad en cualquier período de tiempo determinado.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Para determinar los requisitos de almacenamiento, averiguar cuántos datos que se va a almacenar en el servidor de copia de seguridad en cualquier período de tiempo determinado.<br /><br />Los datos de copia de seguridad se almacenan en el servidor de copia de seguridad en un formato comprimido. Las tasas de compresión de datos dependen de las características de los datos.<br /><br />Por ejemplo: como una estimación aproximada, se recomienda calcular una razón de compresión de 7:1 en relación con el tamaño de los datos sin comprimir. Se supone que al menos el 80% de los datos se almacena en los índices de almacén de columnas agrupado. Por ejemplo, si tiene 700 GB de datos sin comprimir en una base de datos y se almacena en los índices de almacén de columnas agrupado, a continuación, se pudo calcular que la copia de seguridad de base de datos deberá cerca de 100 GB.<br /><br />Si piensa tener varias copias de las copias de seguridad de base de datos en el servidor de copia de seguridad, debe tener en cuenta para ellos.<br /><br />Por ejemplo: si piensa hacer copia de seguridad de 10 bases de datos que contienen cada 5 TB de datos sin comprimir, las bases de datos tienen un tamaño combinado de 50 TB. Si planea estos diario de 10 bases de datos de copia de seguridad durante 5 días en una fila, el tamaño total sin comprimir es 250 TB. Factorizar en una razón de compresión de 7:1, necesitará 250 / 7 = 35.7 TB de almacenamiento en el servidor de copia de seguridad. Se recomienda ser conservador y obtener sobre capacidad adicional de 30% para las variaciones de la cuenta y crecer.  En este ejemplo, sería mejor 46,6 TB.|  
|Red|Tipo de conexión de red.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Determinar el mejor tipo de conexión de red que puede satisfacer los requisitos de velocidad de carga.<br /><br />Por ejemplo: InfiniBand o las tasas de carga de 10 Gigabit Ethernet proporcionará el óptimo. Ethernet de 1 Gigabit limitará las tasas de carga a 360 GB por hora o menos.|  
|E/S|Bytes por hora para operaciones de escritura.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Para escribir las copias de seguridad en disco, 4 TB por hora velocidades de escritura sean óptimas.<br /><br />Por ejemplo: para las unidades que pueden escribir los 50 MB/s, le interesará al menos 24 unidades de disco, además de más de creación de reflejo o paridad.<br /><br />La capacidad de E/S, se tienen en cuenta todas las i/OS ocurre en el servidor de carga. Si el servidor de carga tiene otro tráfico de E/S además de cargas de datos, como la recepción de archivos de datos desde un servidor ETL, aumentarán los requisitos de E/S.|  
|CPU|Número de sockets.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Recibir y almacenar archivos de copia de seguridad no es una aplicación intensiva de CPU.  Como mínimo, se recomienda utilizar un servidor de socket de 2 de los equipos fabricados.|  
|RAM|GB de memoria que permite a Windows en caché los archivos durante la carga.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Recibir y almacenar archivos de copia de seguridad requieren muy poca RAM en el servidor de carga.<br /><br />Para determinar los requisitos de RAM, hacen referencia a la instalación de Windows Server y los requisitos de la aplicación de entidad 3rd. Se recomienda un mínimo de 32 GB si no tiene requisitos de otros orígenes.|  
  
Cuando haya terminado de determinar los requisitos de capacidad, volver a la [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md) tema para planear la compra.  
  
## <a name="see-also"></a>Vea también  
[Copia de seguridad y la carga de hardware](backup-and-loading-hardware.md)  
  
