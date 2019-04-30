---
title: Planeamiento de capacidad de servidor de copia de seguridad - almacenamiento de datos paralelos | Microsoft Docs
description: Esta hoja de cálculo de planeación de capacidad le ayuda a determinar los requisitos para un servidor de copia de seguridad para realizar la copia de seguridad de base de datos de almacenamiento de datos paralelos y las operaciones de restauración. Utilícelo para crear el plan de compras nuevos o aprovisionamiento copia de seguridad servidores existentes.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 500bebab375a0d0b94032a1855af3844bc2e6fa7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63295060"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>Hoja de cálculo de planeación de capacidad de copia de seguridad de servidor: almacenamiento de datos paralelos
Esta hoja de cálculo de planeación de capacidad le ayuda a determinar los requisitos para un servidor de copia de seguridad para realizar la copia de seguridad de base de datos PDW de SQL Server y las operaciones de restauración. Utilícelo para crear el plan de compras nuevos o aprovisionamiento copia de seguridad servidores existentes.  
  
Esta hoja de cálculo es un suplemento de las instrucciones de [adquirir y configurar un servidor de copia de seguridad](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Hoja de planificación de capacidad para los servidores de copia de seguridad  

### <a name="notes"></a>Notas  
  
1.  Esta hoja de cálculo se aplica a los servidores que se va a realizar las operaciones de copia de seguridad y restauración para bases de datos PDW.  
  
2.  Es la única manera de copia de seguridad y restaurar bases de datos PDW utilizar los comandos de base de datos de copia de seguridad y restauración de base de datos SQL. Sin embargo, una vez que los datos de copia de seguridad en el servidor de copia de seguridad, existe como un conjunto de archivos de Windows. Puede archivar los archivos de copia de seguridad desde el servidor a otra ubicación de almacenamiento mediante el uso de métodos copia de seguridad tradicionales de Windows basados en archivos.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Icono del Portapapeles](media/clipboard-icon.png "icono del Portapapeles") hoja de cálculo de planeamiento de capacidad 
  
Imprimir esta hoja de cálculo y rellenarlo con sus propios requisitos.  
  
|Componente|Requisito|Rellene esta columna con sus propios requisitos|Recomendaciones|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Storage|Número máximo de bytes que vaya a almacenar en el servidor de copia de seguridad en cualquier período de tiempo determinado.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Para determinar los requisitos de almacenamiento, averigüe cuántos datos que va a almacenar en el servidor de copia de seguridad en cualquier período de tiempo determinado.<br /><br />Los datos de copia de seguridad se almacenan en el servidor de copia de seguridad en un formato comprimido. Las tasas de compresión de datos dependen de las características de los datos.<br /><br />Por ejemplo: Como una estimación aproximada, se recomienda calcular una proporción de compresión de 7:1 en relación con el tamaño de los datos sin comprimir. Esto supone al menos el 80% de los datos se almacenan en los índices de almacén de columnas agrupado. Por ejemplo, si tiene 700 GB de datos sin comprimir en una base de datos y se almacena en los índices de almacén de columnas agrupado, a continuación, se podría calcular que la copia de seguridad de base de datos necesitará aproximadamente 100 GB.<br /><br />Si planea tener varias copias de las copias de seguridad de base de datos en el servidor de copia de seguridad, debe tener en cuenta para ellos.<br /><br />Por ejemplo: Si tiene previsto realizar copias de seguridad de 10 bases de datos que contienen cada 5 TB de datos sin comprimir, las bases de datos tienen un tamaño combinado de 50 TB. Si tiene previsto realizar copias de seguridad diarias de estas 10 bases de datos durante 5 días en una fila, el tamaño total sin comprimir es 250 TB. La factorización de una relación de compresión de 7:1, tendrá 250 / 7 = 35.7 TB de almacenamiento en el servidor de copia de seguridad. Se recomienda ser conservador y obtener sobre capacidad adicional de 30% para las variaciones de la cuenta y crecer.  En este ejemplo, sería mejor 46,6 TB.|  
|red|Tipo de conexión de red.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Determinar el mejor tipo de conexión de red que pueda satisfacer los requisitos de velocidad de carga.<br /><br />Por ejemplo: InfiniBand o 10 Gbit Ethernet proporcionará el óptimo al cargar las tasas. Ethernet de 1 Gbit limitará las tasas de carga a 360 GB por hora o menos.|  
|E/S|Bytes por hora para operaciones de escritura.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Para escribir copias de seguridad en disco, 4 TB por hora de velocidad de escritura es óptimas.<br /><br />Por ejemplo: Para las unidades que se pueden escribir a 50 MB/s, le interesará al menos 24 unidades de disco, además de otras cuestiones para la creación de reflejo o paridad.<br /><br />Para la capacidad de E/S, se tienen en cuenta todas las operaciones de E/S que se producen en el servidor de carga. Si el servidor de carga tiene otro tráfico de E/S, además de cargas de datos, como la recepción de archivos de datos de un servidor ETL, los requisitos de E/S aumentará.|  
|CPU|Número de sockets.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Recibir y almacenar los archivos de copia de seguridad no es una aplicación de la CPU.  Como mínimo, se recomienda usar un servidor de socket de 2 de los equipos fabricados.|  
|RAM|GB de memoria que permite a Windows en caché los archivos durante la carga.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Recibir y almacenar los archivos de copia de seguridad requieren muy poca RAM en el servidor de carga.<br /><br />Para determinar los requisitos de RAM, consulte la instalación de Windows Server y los requisitos de aplicación parte 3ª. Se recomienda un mínimo de 32 GB, si no tiene requisitos de otros orígenes.|  
  
Cuando haya terminado de determinación de los requisitos de capacidad, volver a la [adquirir y configurar un servidor al cargar](acquire-and-configure-loading-server.md) tema para planear la compra.  
  
## <a name="see-also"></a>Vea también  
[Copia de seguridad y la carga de hardware](backup-and-loading-hardware.md)  
  
