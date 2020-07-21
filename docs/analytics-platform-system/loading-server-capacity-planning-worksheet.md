---
title: Cargando el planeamiento de la capacidad del servidor
description: Esta hoja de cálculo de planeamiento de capacidad le ayuda a determinar los requisitos de un servidor de carga para cargar datos en el almacenamiento de datos paralelos del sistema de análisis de plataforma.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1d2c3f1c0366d2c7d3d9efe700d9cfccc688dbc9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78171604"
---
# <a name="loading-server-capacity-planning-worksheet-for-analytics-platform-system"></a>Cargando hoja de cálculo de planeamiento de capacidad del servidor para Analytics Platform System
Esta hoja de cálculo de planeamiento de capacidad le ayuda a determinar los requisitos de un servidor de carga para cargar datos en PDW de SQL Server. Úselo para crear el plan de compra o aprovisionamiento de servidores de carga existentes.

## <a name="worksheet-notes"></a>Notas de la hoja de cálculo

1.  Esta hoja de cálculo se aplica a los servidores que van a cargar datos con la herramienta de carga de línea de comandos **dwloader** .

2.  Para cargar datos con Integration Services o una herramienta de carga de terceros, los requisitos pueden variar en función de las diferencias en el proceso de carga.

3.  La mayoría de los requisitos se aplican a la carga de archivos de datos comprimidos o sin comprimir; las diferencias en los requisitos se indican en negrita.

## <a name="clipboard-capacity-planning-worksheet"></a>![Portapapeles](media/clipboard-icon.png "Portapapeles") Hoja de cálculo de planeamiento de capacidad

Imprima esta hoja de cálculo y rellénelo con sus propios requisitos.

|Componente|Requisito|Rellene esta columna con sus propios requisitos|Recomendaciones|
|-------------|---------------|--------------------------------------------------|-------------------|
|Storage|Número máximo de bytes que se van a almacenar en el servidor de carga en un período de tiempo determinado.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Para determinar los requisitos de almacenamiento, averigüe la cantidad de datos que planea almacenar en el servidor de carga en un período de tiempo determinado.  Los requisitos de capacidad son solo para cargar archivos; el sistema operativo y los archivos de carga deben estar en matrices de disco diferentes.<br /><br />Por ejemplo: Si tiene previsto cargar 100 GB de datos del disco 3 veces al día, pero no elimina los archivos de datos hasta el final de la semana, necesitará un mínimo de 2,1 TB para almacenar los archivos de datos. Se recomienda ser conservador y obtener un 30% más de almacenamiento para tener en cuenta las variaciones y el crecimiento.  En este ejemplo, se mejoran 2,73 TB de espacio de almacenamiento.|
|Velocidad de carga|Número máximo de bytes por hora de los datos que se van a cargar en PDW.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Esta es una estimación. Al calcular este requisito, supongamos que los archivos ya están en el servidor de carga y que otras condiciones de carga son lo más adecuadas posible.<br /><br />Por ejemplo: no es necesario factorizar en los datos compresión, ya que dwloader siempre envía datos sin comprimir al PDW. No es necesario factorizar en conversiones de tipos de datos y el tamaño de la tabla de destino.|
|Red|Tipo de conexión de red.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Determine el mejor tipo de conexión de red para los requisitos de velocidad de carga.<br /><br />Por ejemplo: InfiniBand o 10 Gbit Ethernet proporcionarán las tasas de carga óptimas. 1 Gbit Ethernet limitará las velocidades de carga a 360 GB por hora o menos.|
|E/S|Bytes por hora para lecturas y escrituras.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Para cargar datos, dwloader debe leer todos los datos del disco antes de enviarlos a PDW.<br /><br />Cada servidor de carga no puede cargar datos más rápido de lo que el dispositivo puede recibir datos de todos los orígenes de carga. Para ahorrar dinero, planee la capacidad de lectura de e/s para la carga de modo que no supere la capacidad de carga del dispositivo.<br /><br />Por ejemplo:<br />PDW recibe y carga datos en una aplicación de 1 bastidor a una velocidad máxima de 1,8 TB por hora. Para un dispositivo con 2 o más bastidores, la velocidad de carga máxima es de 3,6 TB por hora.<br /><br />Si planea cargar desde varios servidores de carga al mismo tiempo, los requisitos de e/s para cada servidor de carga serán menores que cuando un servidor está realizando toda la carga.<br /><br />Por ejemplo: un servidor de carga puede cargar un máximo de 1,8 TB por hora para una aplicación de 1 bastidor. Dos servidores de carga pueden cargar cada simultáneamente 900 GB por hora en un dispositivo de un bastidor. Los niveles más altos de simultaneidad pueden reducir la eficacia y el rendimiento máximo.<br /><br />En cuanto a la capacidad de e/s, tenga en cuenta todas las e/s que se producen en el servidor de carga. Si el servidor de carga tiene otro tráfico de e/s además de las cargas de datos, como recibir archivos de datos de un servidor ETL, aumentarán los requisitos de e/s.<br /><br />En el caso de los datos comprimidos, los requisitos de e/s dependen de la tasa de compresión de datos. dwloader Lee los datos comprimidos y los descomprime antes de enviarlos a PDW. Cuanto mayor sea la relación de compresión, menos datos tendrá que leer el servidor de carga en el disco.<br /><br />Por ejemplo: Si la velocidad de carga necesaria es de 1,8 TB por hora, y los datos se almacenan en el servidor de carga con compresión 2:1, el servidor de carga solo necesita leer 900 GB por hora desde el disco en lugar de 1,8 TB. Una relación de compresión 3:1 significa que el servidor de carga debe leer 600 GB por hora desde el disco.|
|CPU|Número de Sockets.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|Para cargar datos sin comprimir, dwloader no es una aplicación que consume mucha CPU.  Como requisito mínimo, se recomienda usar un servidor de 2 sockets fabricado recientemente.<br /><br />Para cargar datos comprimidos, necesita suficiente capacidad de CPU para descomprimir los datos antes de enviarlos a PDW. dwloader puede ejecutar 10 subprocesos activos a la vez. Si tiene previsto cargar 10 archivos comprimidos simultáneamente, se recomienda que el servidor tenga al menos una CPU de 10 núcleos o dos CPU de 6 núcleos.|
|RAM|GB de memoria que permite a Windows almacenar en caché los archivos durante las cargas.|![Icono de lápiz](media/pencil-icon.png "Icono de lápiz")|dwloader usa muy poca RAM en el servidor de carga. Para el rendimiento, Windows usa la memoria para almacenar en caché los archivos de carga después de leerlos desde el disco.<br /><br />Para determinar los requisitos de RAM, consulte la instalación de Windows Server y los requisitos de las aplicaciones de terceros. Se recomienda un mínimo de 32 GB si no tiene requisitos de otros orígenes.<br /><br />En el caso de los datos comprimidos, la memoria RAM más rápida es útil porque acelerará la descompresión.|

## <a name="see-also"></a>Consulte también
[Adquisición y configuración de un](acquire-and-configure-loading-server.md)
[cargador de línea de comandos dwloader del](dwloader.md) servidor de carga

