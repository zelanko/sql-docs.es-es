---
title: Planeamiento de la capacidad del servidor de copia de seguridad
description: Esta hoja de cálculo de planeamiento de capacidad le ayuda a determinar los requisitos de un servidor de copia de seguridad para realizar operaciones de copia de seguridad y restauración de bases de datos de almacenamiento de datos paralelas. Úselo para crear el plan de compra de servidores de copia de seguridad existentes nuevos o de aprovisionamiento.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 46dbdded5adf41a847f017cf4ee203597df13962
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401342"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>Hoja de cálculo de planeamiento de capacidad del servidor de copia de seguridad-almacenamiento de datos paralelo
Esta hoja de cálculo de planeamiento de capacidad le ayuda a determinar los requisitos de un servidor de copia de seguridad para realizar PDW de SQL Server operaciones de copia de seguridad y restauración de bases de datos. Úselo para crear el plan de compra de servidores de copia de seguridad existentes nuevos o de aprovisionamiento.  
  
Esta hoja de cálculo es un complemento de las instrucciones de [adquisición y configuración de un servidor de copia de seguridad](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Hoja de cálculo de planeamiento de capacidad para servidores de copia de seguridad  

### <a name="notes"></a>Notas  
  
1.  Esta hoja de cálculo se aplica a los servidores que realizarán operaciones de copia de seguridad y restauración de bases de datos de PDW.  
  
2.  La única forma de realizar copias de seguridad y restaurar bases de datos de PDW es usar los comandos de SQL Database BACKUP y RESTOre DATABASE. Sin embargo, una vez que los datos de copia de seguridad están en el servidor de copia de seguridad, existen como un conjunto de archivos de Windows. Puede archivar los archivos de copia de seguridad del servidor en otra ubicación de almacenamiento mediante los métodos tradicionales de copia de seguridad basados en archivos de Windows.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Icono del portapapeles](media/clipboard-icon.png "Icono del portapapeles") Hoja de cálculo de planeamiento de capacidad 
  
Imprima esta hoja de cálculo y rellénelo con sus propios requisitos.  
  
|Componente|Requisito|Rellene esta columna con sus propios requisitos|Recomendaciones|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Storage|Número máximo de bytes que se van a almacenar en el servidor de copia de seguridad en un período de tiempo determinado.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Para determinar los requisitos de almacenamiento, averigüe la cantidad de datos que planea almacenar en el servidor de copia de seguridad en un período de tiempo determinado.<br /><br />Los datos de copia de seguridad se almacenan en el servidor de copia de seguridad en un formato comprimido. Las tasas de compresión de datos dependen de las características de los datos.<br /><br />Por ejemplo: como estimación aproximada, se recomienda calcular una relación de compresión 7:1 en relación con el tamaño de los datos sin comprimir. Esto supone que al menos el 80% de los datos se almacenan en los índices de almacén de columnas agrupados. Por ejemplo, si tiene 700 GB de datos sin comprimir en una base de datos y se almacenan en índices de almacén de columnas agrupados, puede calcular la copia de seguridad de la base de datos necesitará aproximadamente 100 GB.<br /><br />Si planea tener varias copias de las copias de seguridad de base de datos en el servidor de copia de seguridad, debe tener en cuenta estas.<br /><br />Por ejemplo: Si planea realizar una copia de seguridad de 10 bases de datos que contienen cada una de 5 TB de datos sin comprimir, las bases de datos tienen un tamaño combinado de 50 TB. Si planea realizar una copia de seguridad de estas 10 bases de datos cada día durante 5 días en una fila, el tamaño total sin comprimir es 250 TB. Factorización en una relación de compresión 7:1, necesitará 250/7 = 35,7 TB de almacenamiento en el servidor de copia de seguridad. Se recomienda ser conservador y obtener un 30% de capacidad adicional para tener en cuenta las variaciones y el crecimiento.  En este ejemplo, 46,6 TB sería mejor.|  
|Red|Tipo de conexión de red.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Determine el mejor tipo de conexión de red que puede cumplir los requisitos de velocidad de carga.<br /><br />Por ejemplo: InfiniBand o Ethernet 10 Gbit proporcionarán las tasas de carga óptimas. Uno Ethernet limitará las velocidades de carga a 360 GB por hora o menos.|  
|E/S|Bytes por hora para las escrituras.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Para escribir copias de seguridad en disco, la velocidad de escritura de 4 TB por hora es óptima.<br /><br />Por ejemplo: en el caso de las unidades que pueden escribir 50 MB/s, querrá al menos 24 unidades, más para la creación de reflejo o paridad.<br /><br />En cuanto a la capacidad de e/s, tenga en cuenta todas las e/s que se producen en el servidor de carga. Si el servidor de carga tiene otro tráfico de e/s además de las cargas de datos, como recibir archivos de datos de un servidor ETL, aumentarán los requisitos de e/s.|  
|CPU|Número de Sockets.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Recibir y almacenar archivos de copia de seguridad no es una aplicación que consume mucha CPU.  Como requisito mínimo, se recomienda usar un servidor de 2 sockets fabricado recientemente.|  
|RAM|GB de memoria que permite a Windows almacenar en caché los archivos durante las cargas.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|La recepción y el almacenamiento de archivos de copia de seguridad requieren muy poca memoria RAM en el servidor de carga.<br /><br />Para determinar los requisitos de RAM, consulte la instalación de Windows Server y los requisitos de las aplicaciones de terceros. Se recomienda un mínimo de 32 GB si no tiene requisitos de otros orígenes.|  
  
Cuando haya terminado de determinar los requisitos de capacidad, vuelva al tema [adquisición y configuración de un servidor de carga](acquire-and-configure-loading-server.md) para planear la compra.  
  
## <a name="see-also"></a>Véase también  
[Copia de seguridad y carga de hardware](backup-and-loading-hardware.md)  
  
