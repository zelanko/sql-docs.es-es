---
title: "Carga la hoja de planificación capacidad de servidor (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Esta hoja de cálculo de planeación de capacidad le ayudará a determinar los requisitos para un servidor de carga para cargar datos en SQL Server PDW."
ms.date: 01/05/2017
ms.topic: article
ms.assetid: df2155be-a624-40ba-9a85-58af708f7ce7
caps.latest.revision: "9"
ms.openlocfilehash: e14d4baca91e0b892b84620330655271fa67badb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="loading-server-capacity-planning-worksheet"></a>Carga la hoja de planificación de capacidad de servidor
Esta hoja de cálculo de planeación de capacidad le ayudará a determinar los requisitos para un servidor de carga para cargar datos en SQL Server PDW. Utilícelo para crear un plan para adquirir o aprovisionamiento existente cargar servidores.  
  
## <a name="worksheet-notes"></a>Notas de la hoja de cálculo
  
1.  Esta hoja de cálculo se aplica a los servidores que se pueden cargar los datos con la **dwloader** herramienta de carga de la línea de comandos.  
  
2.  Para cargar los datos con Integration Services o una herramienta de carga de entidades, los requisitos pueden variar en función de las diferencias en el proceso de carga.  
  
3.  La mayoría de los requisitos se aplica a la carga de ambos archivos de datos comprimidos o sin comprimir; las diferencias en los requisitos se indican en negrita.  
  
## <a name="clipboardmediaclipboard-iconpng-clipboard-capacity-planning-worksheet"></a>![Portapapeles](media/clipboard-icon.png "Portapapeles") hoja de cálculo de planificación de capacidad  
  
Imprimir esta hoja de cálculo y rellenarlo con sus propios requisitos.  
  
|Componente|Requisito|Rellene esta columna con sus propios requisitos|Recomendaciones|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Almacenamiento|Número máximo de bytes que vaya a almacenar en el servidor de carga en cualquier período de tiempo determinado.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Para determinar los requisitos de almacenamiento, averiguar cuántos datos que se va a almacenar en el servidor de carga en cualquier período de tiempo determinado.  Son los requisitos de capacidad de cargar archivos solo; el sistema operativo y los archivos de carga deben estar en matrices de disco diferente.<br /><br />Por ejemplo: si piensa cargar 100 GB de datos desde el disco 3 veces al día, pero no elimina los archivos de datos hasta el final de la semana, necesita un mínimo 2,1 TB para almacenar los archivos de datos. Se recomienda ser conservador y obtener sobre almacenamiento de más de 30% para tener en cuenta las variaciones y crecimiento.  En este ejemplo, sería mejor 2,73 TB de espacio de almacenamiento.|  
|Velocidad de carga|Número máximo de bytes por hora de datos que se va a cargar en PDW.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Esta es una estimación. Al calcular este requisito, suponga que los archivos ya están en el servidor de carga, y que otras condiciones de carga son tan buenos como sea posibles.<br /><br />Por ejemplo: sin necesidad de tener capacidad de compresión de datos ya que dwloader siempre envía los datos sin comprimir al PDW en. No es necesario tener en cuenta las conversiones de tipo de datos y el tamaño de la tabla de destino.|  
|Red|Tipo de conexión de red.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Determinar el mejor tipo de conexión de red para los requisitos de velocidad de carga.<br /><br />Por ejemplo: InfiniBand o 10 Gigabit Ethernet proporcionará las tasas de carga óptimo. Ethernet de 1 Gbit limitará las tasas de carga a 360 GB por hora o menos.|  
|E/S|Bytes por hora para las lecturas y escrituras.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Para cargar datos, dwloader debe leer todos los datos del disco antes de enviarlo a PDW.<br /><br />Cada servidor de carga no puede cargar datos mucho más rápido que el dispositivo puede recibir datos de todos los orígenes de carga. Para ahorrar dinero, planee la capacidad para cargar por lo que no supera la capacidad de carga del dispositivo de lectura de entrada/salida.<br /><br />Por ejemplo:<br />PDW recibe y carga datos en un dispositivo de bastidor de 1 a una velocidad máxima de 1,8 TB por hora. Para un dispositivo con 2 o más racks, la velocidad de carga máxima es de 3,6 TB por hora.<br /><br />Si va a cargar desde varios servidores de carga al mismo tiempo, los requisitos de E/S para cada servidor de carga será menor que cuando un servidor está realizando todas la carga.<br /><br />Por ejemplo: un servidor de carga puede cargar un máximo de 1,8 TB por hora para un dispositivo de bastidor de 1. Dos servidores de carga podrían cada carguen simultáneamente 900 GB por hora en un dispositivo de bastidor de 1. Niveles más altos de simultaneidad pueden reducir la eficacia y el rendimiento máximo.<br /><br />La capacidad de E/S, se tienen en cuenta todas las i/OS ocurre en el servidor de carga. Si el servidor de carga tiene otro tráfico de E/S además de cargas de datos, como la recepción de archivos de datos desde un servidor ETL, aumentarán los requisitos de E/S.<br /><br />Los requisitos de E/S para los datos comprimidos, dependen de la tasa de compresión de datos. dwloader lee los datos comprimidos y, a continuación, se descomprime antes de enviarlo a PDW. Cuanto mayor sea la razón de compresión, menos datos cargando servidor necesitará leer del disco.<br /><br />Por ejemplo: si la velocidad de carga necesario es 1,8 TB por hora y los datos se almacenan en el servidor de carga con la compresión de 2:1, a continuación, el servidor de carga sólo necesita leer 900 GB por hora desde el disco en lugar de 1,8 TB. Una razón de compresión de 3:1 significa que el servidor de carga necesita leer 600 GB por hora desde el disco.|  
|CPU|Número de sockets.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|Para cargar datos sin comprimir, dwloader no es una aplicación intensiva de CPU.  Como mínimo, se recomienda utilizar un servidor de socket de 2 de los equipos fabricados.<br /><br />Para cargar los datos comprimidos, necesita suficiente capacidad de CPU para descomprimir los datos antes de enviarlo a PDW. dwloader puede ejecutar al mismo tiempo 10 subprocesos activos. Si tiene previsto cargar al mismo tiempo 10 archivos comprimidos, se recomienda que el servidor tiene al menos una CPU de núcleo de 10 o dos de 6 núcleos CPU.|  
|RAM|GB de memoria que permite a Windows en caché los archivos durante la carga.|![Icono de lápiz](media/pencil-icon.png "icono de lápiz")|dwloader utiliza muy poco RAM en el servidor de carga. Para obtener un rendimiento, Windows utiliza memoria para almacenar en caché los archivos de carga después de leerlos desde el disco.<br /><br />Para determinar los requisitos de RAM, hacen referencia a la instalación de Windows Server y los requisitos de la aplicación de entidad 3rd. Se recomienda un mínimo de 32 GB si no tiene requisitos de otros orígenes.<br /><br />Para los datos comprimidos, RAM, más rápida es útil porque acelerará la descompresión.|  
  
## <a name="see-also"></a>Vea también  
[Adquisición y configuración de servidores de carga](acquire-and-configure-loading-server.md)  
[Cargador de la línea de comandos de dwloader](dwloader.md)  
  
