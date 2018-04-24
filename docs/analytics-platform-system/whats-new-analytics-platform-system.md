---
title: 'Novedades de Analytics Platform System: un almacén de datos de escala horizontal | Documentos de Microsoft'
description: Vea cuáles son las novedades en Microsoft® Analytics Platform System, un dispositivo de escalado horizontal local que hospeda el almacenamiento de datos paralelos de MPP de SQL Server.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4beb44ac45d95aa0338dc9dc0be0796a223d3243
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="whats-new-in-analytics-platform-system-2016-a-scale-out-mpp-data-warehouse"></a>Novedades de análisis de plataforma System 2016, un almacén de datos MPP de escalabilidad horizontal
Vea cuáles son las novedades en Microsoft® Analytics Platform System (APS) 2016, la última actualización de dispositivo para un dispositivo de escalado horizontal local que hospeda el almacenamiento de datos paralelos de MPP de SQL Server. 

## <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 se ejecuta en la versión más reciente de SQL Server 2016 y usa el nivel de compatibilidad de base de datos predeterminado 130.  SQL Server 2016 hace posible admitir algunas de las nuevas características, como los índices secundarios para los índices de almacén de columnas agrupado y Kerberos para PolyBase. 


## <a name="t-sql"></a>T-SQL
APS 2016 admite estas mejoras de compatibilidad de T-SQL.  Estos elementos adicionales del lenguaje sea más fácil migrar de SQL Server y otros orígenes de datos. 

- [Intercalaciones de SQL de nivel de columna][] ahora se admiten además de las intercalaciones de Windows.
- [Índices no clúster en índices de almacén de columnas agrupado][] mejorar el rendimiento de las consultas que buscan valores específicos en el índice de almacén de columnas agrupado. 
- [SELECCIONE... EN][] 
- [sp_spaceused()][] muestra el espacio en disco utilizado o reservado en una tabla o una base de datos.
- [Tablas anchas][] soporte es el mismo que SQL Server 2016. El límite de 32K anterior para el tamaño de fila ya no existe. 

### <a name="data-types"></a>Tipos de datos

- [Varchar (max)][], [nvarchar (max)][] y [varbinary (max)][]. Estos tipos de datos LOB tienen un tamaño máximo de 2 GB. Para cargar estos objetos utilizan [bcp (utilidad)][]. Polybase y dwloader no admiten actualmente estos tipos de datos. 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [NUMÉRICO][] y tipos de datos DECIMAL.

### <a name="window-functions"></a>Funciones de ventana

- [ROWS o RANGE][] en la cláusula OVER de la instrucción SELECT.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

### <a name="security-functions"></a>Funciones de seguridad

- [Checksum()][] y [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

### <a name="additional-functions"></a>Funciones adicionales

- [NEWID()][]
- [RAND][]

## <a name="polybasehadoop-enhancements"></a>Mejoras de PolyBase/Hadoop

- Compatibilidad con Hortonworks HDP 2.4 y HDP 2.5
- Compatibilidad con Kerberos a través de credenciales de ámbito de la base de datos
- Compatibilidad con la credencial con Blobs de almacenamiento de Azure

## <a name="install-and-upgrade-enhancements"></a>Instalación y actualización mejoras

### <a name="enterprise-architecture-updates"></a>Actualizaciones de arquitectura de empresa
Actualizar el dispositivo existente a APS 2016 instala el firmware más reciente y actualizaciones de controladores, que incluyen revisiones de seguridad. 

Un nuevo dispositivo de HPE o DELL incluye todas las actualizaciones más recientes más:

- Compatibilidad de procesador de última generación (Broadwell)
- Actualizar a DDR4 DIMM
- Mejorar el rendimiento DIMM

### <a name="integration"></a>Integración

- Compatibilidad con el nombre de dominio completo (FQDN) totalmente permite configurar una confianza de dominio para el dispositivo. 
- Para usar FQDN, debe realizar una actualización completa y darse de alta durante la actualización. 

### <a name="reduced-downtime"></a>Menor tiempo de inactividad
Instalar o actualizar a APS 2016 es más rápido y requiere menos tiempo de inactividad que las versiones anteriores. Para reducir el tiempo de inactividad, la instalación o una actualización: 

 - Optimiza aplicar actualizaciones WSUS mediante el uso de una imagen que contiene todas las actualizaciones a través de junio de 2016
 - Se aplica a las actualizaciones de seguridad con las actualizaciones de controladores y firmware
 - Coloca las revisiones más recientes y la utilidad de comprobación de dispositivo (PAV) en el dispositivo para que estén preparados instalar sin necesidad de descargarlos.


<!--MSDN references-->
[database compatibility level 130]:https://msdn.microsoft.com/library/bb510680.aspx
[Intercalaciones de SQL de nivel de columna]:https://msdn.microsoft.com/library/ms143726.aspx
[Índices no clúster en índices de almacén de columnas agrupado]:https://msdn.microsoft.com/library/ms188783.aspx
[Varchar (max)]:https://msdn.microsoft.com/library/ms176089.aspx
[nvarchar (max)]:https://msdn.microsoft.com/library/ms186939.aspx
[varbinary (max)]:https://msdn.microsoft.com/library/ms188362.aspx
[SYSNAME]:https://msdn.microsoft.com/library/ms188021.aspx
[SELECCIONE... EN]:https://msdn.microsoft.com/library/ms188029.aspx
[sp_spaceused()]:https://msdn.microsoft.com/library/ms188776.aspx
[Tablas anchas]:https://msdn.microsoft.com/library/ms143432.aspx
[BULK INSERT]:https://msdn.microsoft.com/library/ms188365.aspx
[bcp (utilidad)]:https://msdn.microsoft.com/library/ms162802.aspx
[UNIQUEIDENTIFIER]:https://msdn.microsoft.com/library/ms187942.aspx
[NUMÉRICO]:https://msdn.microsoft.com/library/ms187746.aspx
[ROWS o RANGE]:https://msdn.microsoft.com/library/ms189461.aspx
[FIRST_VALUE]:https://msdn.microsoft.com/library/hh213018.aspx
[LAST_VALUE]:https://msdn.microsoft.com/library/hh231517.aspx
[CUME_DIST]:https://msdn.microsoft.com//library/hh231078.aspx
[PERCENT_RANK]:https://msdn.microsoft.com/library/hh213573.aspx
[Checksum()]:https://msdn.microsoft.com/library/ms189788.aspx
[BINARY_CHECKSUM()]:https://msdn.microsoft.com/library/ms173784.aspx
[HAS_PERMS_BY_NAME()]:https://msdn.microsoft.com/library/ms189802.aspx
[NEWID()]:https://msdn.microsoft.com/library/ms190348.aspx
[RAND]:https://msdn.microsoft.com/library/ms177610.aspx


  

  


