---
title: "Usar sqlBindR.exe para actualizar una instancia de R Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server (starting with 2016 CTP3)"
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Usar sqlBindR.exe para actualizar una instancia de R Services
Microsoft R Server para Windows contiene una nueva herramienta, denominada **SqlBindR.exe**, que se puede usar para actualizar los componentes de R de una instancia. Este proceso se denomina **enlace**, debido a que cambia el modelo de licencia para que una instancia de SQL Server 2016 use la nueva licencia de compatibilidad del ciclo de vida de software moderno de Microsoft.

En general, este sistema de licencias garantiza que los científicos de datos siempre usen la versión más reciente de R. Para obtener más información sobre los términos y las ventajas de la licencia de software de Microsoft, consulte [Run Microsoft R Server for Windows](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev) (Ejecutar Microsoft R Server para Windows).

Al enlazar una instancia, ocurren tres cosas:
+ La directiva de compatibilidad de la instancia cambia de la directiva de compatibilidad de SQL Server 2016 al nuevo contrato de licencia de software moderno de Microsoft.
+ Los componentes de R asociados a esa instancia se actualizarán automáticamente con cada versión, junto con la versión de R Server que actualmente contemplan los nuevos términos de licencia de software moderno.
+ La instancia ya no se puede actualizar manualmente, excepto para agregar paquetes nuevos. 

Si más adelante decide que quiere dejar de actualizar la instancia en cada versión, debe **desenlazar** la instancia y, después, desinstalar los componentes de Microsoft R Server como se describe en este artículo: [Run Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) (Ejecutar Microsoft R Server para Windows). Una vez completado el proceso, las actualizaciones futuras de R Server no afectarán a la instancia.

> [!NOTE] El proceso de actualización solo se admite para las instancias de SQL Server 2016 que se hayan revisado con actualización acumulativa 3.0.  
> 
> Si usa R Services en SQL Server vNext, no es necesario que aplique esta actualización. Los componentes de R siempre se actualizan automáticamente en cada hito.

## <a name="how-to-upgrade-an-instance"></a>Cómo actualizar una instancia


1. Ejecute el instalador de Microsoft R Server en el equipo que tenga la instancia que quiere actualizar.
2. Cuando se complete la instalación, busque la carpeta que contiene la herramienta **SqlBindR.exe**. La ubicación predeterminada es `C:\Program Files\Microsoft\R Server\Setup`
2. Abra un símbolo del sistema como administrador.
3. Escriba el comando siguiente para ver una lista de instancias disponibles: `SqlBindR.exe /list`
4. Ejecute el comando **SqlBindR.exe** con el argumento */bind* para especificar el nombre de la instancia que se va a actualizar. 
   Por ejemplo, para actualizar solo la instancia predeterminada, escriba:  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

## <a name="how-to-downgrade-an-instance-of-r-services"></a>Cómo cambiar una instancia de R Services a una versión anterior

Para revertir el estado de una instancia, debe ejecutar la herramienta SqlBindR para quitar la licencia y, después, debe reparar o reinstalar la instancia.

1. Ejecute el comando **SqlBindR.exe** con el argumento */unbind* y especifique la instancia. 
   Por ejemplo, el comando siguiente revierte la instancia predeterminada para cumplir con la licencia de SQL Server y la programación de actualización de SQL Server:  `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`
2. Para restaurar la instancia a su estado original, realice una de las siguientes acciones:
    + Repare la instancia. La operación de reparación aplicará actualizaciones a todas las funciones instaladas.
    + Desinstale y vuelva a instalar y, después, aplique todas las versiones de servicio. Se debe reiniciar la instancia.
3. Una vez que se haya quitado R Server, también se quitarán todos los paquetes que se instalaron con la instancia y, por lo tanto, se deben volver a instalar.

## <a name="requirements"></a>Requisitos
La actualización solo se admite para las instancias de SQL Server 2016 que cumplen los requisitos siguientes:
+ SQL Server 2016 SP1 o posterior
+ Se ha aplicado la actualización acumulativa 3.0 (OD)

Actualmente solo se admite la actualización mediante la herramienta de línea de comandos. En una versión posterior se proporcionará una interfaz interactiva.

## <a name="sqlbindrexe-command-syntax"></a>Sintaxis de comandos de sqlbindr.exe


### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parámetros

|Nombre|Description|
|------|------|
|*list*| Muestra una lista de todos los identificadores de instancia de SQL Database en el equipo actual.|
|*bind*| Actualiza la instancia de SQL Database especificada a la versión más reciente de R Server y garantiza que la instancia obtenga automáticamente las actualizaciones futuras de R Server.|
|*unbind*|Desinstala la versión más reciente de R Server de la instancia de SQL Database especificada e impide que las actualizaciones futuras de R Server afecten a la instancia.|

### <a name="errors"></a>Errores

La herramienta devuelve los siguientes mensajes de error:

|Error|Solución|
|------|------|
|An error occurred while binding the instance (Se produjo un error al enlazar la instancia)| No se pudo enlazar la instancia. Póngase en contacto con el servicio de soporte técnico para obtener ayuda.|
|The instance is already bound (La instancia ya está enlazada)| Ha ejecutado el comando *bind*, pero la instancia especificada ya está enlazada. Elija una instancia diferente.|
|The instance is not bound (La instancia no está enlazada)| Ha ejecutado el comando *unbind*, pero la instancia especificada no está enlazada. Elija una instancia diferente.|
|Not a valid SQL instance ID (Identificador de instancia de SQL no válido)| Puede que haya escrito el nombre de instancia incorrectamente. Ejecute el comando de nuevo con el argumento *list* para ver los identificadores de instancia disponibles.|
|No se encontraron instancias| Este equipo no tiene una instancia de SQL Server R Services.|
|La instancia debe tener instalada una versión compatible de SQL R Services (en bases de datos).| Consulte https://go.microsoft.com/fwlink/?linkid=835761 para obtener más detalles.|
|An error occurred while unbinding the instance (Se produjo un error al desenlazar la instancia)| No se pudo desenlazar la instancia. Póngase en contacto con el servicio de soporte técnico para obtener ayuda.|
|Error inesperado| Otros errores. Póngase en contacto con el servicio de soporte técnico para obtener ayuda.  |
|No SQL instances found (No se encontraron instancias de SQL)| Este equipo no tiene una instancia de SQL Server. |


## <a name="see-also"></a>Vea también

[R Server Release Notes](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) (Notas de la versión de SQL Server)
