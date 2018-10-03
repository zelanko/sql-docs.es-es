---
title: Especificación de copia de seguridad de VDI, SQL Server en Linux | Microsoft Docs
description: Especificación de interfaz de dispositivo Virtual de copia de seguridad de SQL Server.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: f29a133ce422b5e6fd04bcd6a78bd036e1f447ee
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806183"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server en la especificación de SDK de cliente de Linux VDI

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento describe las interfaces proporcionadas por SQL Server en el SDK de cliente de interfaz (VDI) de dispositivo virtual de Linux. Proveedores de software independientes (ISV) pueden usar el Virtual copia de seguridad de dispositivo aplicación interfaz de programación (API) para integrar SQL Server en sus productos. En general, VDI en Linux se comporta de forma similar a VDI en Windows con los cambios siguientes:

- Memoria compartida de Windows se convierte en la memoria compartida de POSIX.
- Los semáforos de Windows se convierten en POSIX semáforos.
- Tipos de Windows como HRESULT y DWORD se cambian los equivalentes de entero.
- Las interfaces COM que se quitan y reemplazan con un par de clases de C++.
- SQL Server en Linux no admite instancias con nombre, por lo que se han quitado las referencias al nombre de instancia. 
- La biblioteca compartida se implementa en libsqlvdi.so instalado en /opt/mssql/lib/libsqlvdi.so

Este documento es un anexo a **vbackup.chm** que detalla la especificación de VDI de Windows. Descargue el [Windows VDI especificación](http://www.microsoft.com/download/details.aspx?id=17282).

Revise también la solución de copia de seguridad de VDI de ejemplo en el [repositorio de GitHub de ejemplos de SQL Server](http://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux).

## <a name="user-permissions-setup"></a>Configuración de permisos de usuario

En Linux, primitivas POSIX pertenecen al usuario crear estas aplicaciones y su grupo de forma predeterminada. Para los objetos creados por SQL Server, estos predeterminada pertenecerán por el usuario de mssql y el grupo de mssql. Para permitir el uso compartido entre SQL Server y el cliente VDI, se recomienda uno de los dos métodos siguientes:

1. Ejecute al cliente de VDI como el usuario de mssql
   
   Ejecute el siguiente comando para cambiar al usuario de mssql:
   
   ```bash
   sudo su mssql
   ```

2. Agregue el usuario de mssql al grupo de vdiuser y la vdiuser al grupo mssql.
   
   Ejecute los comandos siguientes:

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   Reinicie el servidor a recoger grupos nuevos para SQL Server y vdiuser

## <a name="client-functions"></a>Funciones de cliente

Este capítulo contiene descripciones de cada una de las funciones de cliente. Las descripciones de incluyen la información siguiente:

- Propósito de la función
- Sintaxis de la función
- lista de parámetros
- Valores devueltos
- Comentarios

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**Propósito** esta función crea el conjunto de dispositivos virtuales.

**Sintaxis**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| | **Nombre** | Esto identifica el conjunto de dispositivos virtuales. Se deben seguir las reglas de los nombres utilizados por CreateFileMapping(). Cualquier carácter excepto con barra diagonal inversa (\) puede utilizarse. Se trata de una cadena de caracteres. Se recomienda un prefijo de la cadena con el nombre de producto o compañía y el nombre de base de datos. |
| |**cfg** | Esta es la configuración para el conjunto de dispositivos virtuales. Para obtener más información, consulte "Configuración" más adelante en este documento.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** | La función se ha realizado correctamente. |
| |**VD_E_NOTSUPPORTED** |Uno o varios de los campos en la configuración no eran válido o no se admite en caso contrario. |
| |**VD_E_PROTOCOL** | El dispositivo virtual ya existe.

**Comentarios** crear el método debe llamarse una sola vez por cada operación de copia de seguridad o restauración. Después de invocar al método Close, el cliente puede volver a usar la interfaz para crear otro conjunto de dispositivos virtuales.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**Propósito** esta función se utiliza para esperar el servidor configurar el conjunto de dispositivos virtuales.
**Sintaxis**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| | **Tiempo de espera** | Este es el tiempo de espera en milisegundos. Usar infinito o un número entero negativo para evitar tiempo de espera.
| | **cfg** | Después de ejecutarse correctamente, contiene la configuración seleccionada por el servidor. Para obtener más información, consulte "Configuración" más adelante en este documento.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** | Se devolvió la configuración.
| |**VD_E_ABORT** |Se invocó SignalAbort.
| |**VD_E_TIMEOUT** |La función ha agotado el tiempo de espera.

**Comentarios** esta función bloquea en un estado de alerta. Después de invocarse correcta, se pueden abrir los dispositivos en el conjunto de dispositivos virtuales.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**Propósito** esta función abre uno de los dispositivos en el conjunto de dispositivos virtuales.
**Sintaxis**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| | **Nombre** |Esto identifica el conjunto de dispositivos virtuales.
| | **ppVirtualDevice** |Cuando la función se realiza correctamente, se devuelve un puntero al dispositivo virtual. Este dispositivo se usa para GetCommand y CompleteCommand.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |La función se ha realizado correctamente.
| |**VD_E_ABORT** | Se ha solicitado la anulación.
| |**VD_E_OPEN** |  Todos los dispositivos están abiertos.
| |**VD_E_PROTOCOL** |  El conjunto no está en el estado de inicialización o este dispositivo particular ya está abierto.
| |**VD_E_INVALID** |El nombre del dispositivo no es válido. No es uno de los nombres que se sabe que componen el conjunto.

**Comentarios** VD_E_OPEN puede devolverse sin problema. El cliente puede llamar a OpenDevice por medio de un bucle hasta que se devuelve este código.
Si se configura más de un dispositivo, por ejemplo *n* dispositivos, devolverá el conjunto de dispositivos virtual *n* interfaces de dispositivo único.

El `GetConfiguration` función puede utilizarse para esperar hasta que se pueden abrir los dispositivos.
Si esta función no se realiza correctamente, se devuelve un valor nulo a través de la ppVirtualDevice.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**Propósito** esta función se utiliza para obtener el siguiente comando en cola en un dispositivo. Cuando se solicita, esta función espera para el siguiente comando.

**Sintaxis**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |**Tiempo de espera** |Se trata de tiempo de espera en milisegundos. Use FINITA para esperar indefinidamente. Use 0 para sondear en busca de un comando. VD_E_TIMEOUT se devuelve si no hay ningún comando disponible actualmente. Si se produce el tiempo de espera, el cliente decide la acción siguiente.
| |**Timeout** |Se trata de tiempo de espera en milisegundos. Use FINITA o un valor negativo para esperar indefinidamente. Use 0 para sondear en busca de un comando. VD_E_TIMEOUT se devuelve si no hay ningún comando está disponible antes de que expire el tiempo de espera. Si se produce el tiempo de espera, el cliente decide la acción siguiente.
| |**ppCmd** |Cuando un comando se devuelve correctamente, el parámetro devuelve la dirección de un comando para ejecutar. La memoria devuelta es de solo lectura. Cuando se completa el comando, este puntero se pasa a la rutina CompleteCommand. Para obtener más información acerca de cada comando, vea "Comandos" más adelante en este documento.
        
| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |Se capturó un comando.
| |**VD_E_CLOSE** |El dispositivo se ha cerrado el servidor.
| |**VD_E_TIMEOUT** |Comando no estaba disponible y el tiempo de espera expirado.
| |**VD_E_ABORT** |El cliente o el servidor ha utilizado el SignalAbort para forzar el cierre.

**Comentarios** VD_E_CLOSE cuando se devuelve, SQL Server ha cerrado el dispositivo. Esto forma parte del cierre normal. Después de que se han cerrado todos los dispositivos, el cliente invoca ClientVirtualDeviceSet::Close para cerrar el conjunto de dispositivos virtuales.
Cuando se debe bloquear esta rutina para esperar un comando, el subproceso se deja en una condición de alerta.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**Propósito** esta función se utiliza para notificar la finalización de un comando de SQL Server. Se debe devolver información de finalización adecuado para el comando. Para obtener más información, vea "Comandos" más adelante en este documento.

**Sintaxis** 

   ```
   int ClientVirtualDevice::CompleteCommand (
   VDC_Command pCmd,        // the command
   int  completionCode,     // completion code
   unsigned long    bytesTransferred,   // bytes transferred
   int64_t  position        // current position
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |**pCmd** |Se trata de la dirección de un comando que se devolvió previamente desde ClientVirtualDevice::GetCommand.
| |**completionCode** |Se trata de un código de estado que indica el estado de finalización. Este parámetro debe devolverse para todos los comandos. El código devuelto debe ser adecuado para el comando que se va a realizar. ERROR_SUCCESS se utiliza en todos los casos para denotar un comando ejecutado correctamente. Para obtener la lista completa de posibles códigos, vea el archivo, vdierror.h. Aparece una lista de códigos de estado típico para cada comando en "Commands" más adelante en este documento.
| |**bytesTransferred** |Este es el número de bytes transferidos correctamente. Se devuelve solo la transferencia de datos de comandos de lectura y escritura.
| |**Posición** |Se trata de una respuesta al comando GetPosition solo.
        
| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |Se observó correctamente la finalización.
| |**VD_E_INVALID** |pCmd no era un comando activo.
| |**VD_E_ABORT** |Se ha señalado la anulación.
| |**VD_E_PROTOCOL** |El dispositivo no está abierto.

**Comentarios** ninguno

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**Propósito** esta función se usa para indicar que se debe producir una finalización anormal.

**Sintaxis** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |None | No aplicable
        
| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR**|La notificación de anulación se registró correctamente.

**Comentarios** en cualquier momento, el cliente puede elegir Anular la operación de copia de seguridad o restauración. Esta rutina indica que deben dejar de todas las operaciones. El estado del conjunto de dispositivos virtual entra en un estado anormal. No hay comandos adicionales se devuelven en los dispositivos. Todos los comandos incompletas se completan automáticamente, devolver ERROR_OPERATION_ABORTED como código de finalización. El cliente debe llamar a ClientVirtualDeviceSet::Close después de ha terminado con seguridad cualquier uso pendiente de búferes que se proporcionan al cliente. Para obtener más información, vea "Terminación anómala" anteriormente en este documento.

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**Propósito** esta función cierra el conjunto de dispositivos virtuales creado por ClientVirtualDeviceSet::Create. Se produce en la versión de todos los recursos asociados con el conjunto de dispositivos virtuales.

**Sintaxis** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |None |No aplicable
        
| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |Se devuelve cuando el conjunto de dispositivos virtuales se cerró correctamente.
| |**VD_E_PROTOCOL** |Se realizó ninguna acción porque el conjunto de dispositivos virtual no estaba abierto.
| |**VD_E_OPEN** |Los dispositivos eran sigue abiertos.

**Comentarios** la invocación de cierre es una declaración de cliente que se deben liberar todos los recursos utilizados por el conjunto de dispositivos virtuales. El cliente debe asegurarse de que todas las actividades relacionadas con los búferes de datos y dispositivos virtuales ha finalizado antes de invocar el cierre. Todas las interfaces de dispositivo virtual devueltas por OpenDevice dejan de cierre.
El cliente puede emitir una llamada de creación en la interfaz del conjunto de dispositivos virtual después de que se devuelva la llamada a Close. Una de estas llamadas crearía un nuevo dispositivo virtual establecido para una operación de copia de seguridad o restauración posteriores.
Si se llama a Close cuando uno o más dispositivos virtuales que estén abiertos, se devuelve VD_E_OPEN. En este caso, SignalAbort se internamente desencadena, para garantizar un cierre correcto si es posible. Libera los recursos VDI. El cliente debe esperar para obtener una indicación VD_E_CLOSE en cada dispositivo antes de invocar ClientVirtualDeviceSet::Close. Si el cliente sabe que el conjunto de dispositivos virtual ya está en un estado anormal, entonces no debe esperar una indicación VD_E_CLOSE desde GetCommand y, si puede invocar ClientVirtualDeviceSet::Close tan pronto como finaliza la actividad en los búferes compartidos.
Para obtener más información, vea "Terminación anómala" anteriormente en este documento.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**Propósito** esta función abre el dispositivo virtual configurado en un cliente secundario. El cliente principal debe haber usado ya crear y GetConfiguration para configurar el conjunto de dispositivos virtuales.

**Sintaxis** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |**SetName** |Esto identifica el conjunto. Este nombre distingue mayúsculas de minúsculas y debe coincidir con el nombre utilizado por el cliente principal cuando invoque ClientVirtualDeviceSet::Create.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |La función se ha realizado correctamente.
| |**VD_E_PROTOCOL** |El conjunto de dispositivos virtual no se ha creado, ya ha abierto en este cliente o el dispositivo virtual conjunto no está listo para aceptar las solicitudes abiertas de clientes secundaria.
| |**VD_E_ABORT** |Se ha anulado la operación.

**Comentarios** cuando se usa un modelo de proceso de varias, el cliente principal es responsable de detectar la terminación normal y anómala de clientes secundaria.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**Propósito** algunas aplicaciones pueden requerir más de un proceso para operar en los búferes devueltos por ClientVirtualDevice::GetCommand. En tales casos, el proceso que recibe el comando puede utilizar GetBufferHandle para obtener un identificador de proceso independiente que identifica el búfer. A continuación, se puede comunicar este identificador a cualquier otro proceso que también tenga el mismo abrir el dispositivo Virtual configurado. Ese proceso, a continuación, usaría ClientVirtualDeviceSet::MapBufferHandle para obtener la dirección del búfer. La dirección probablemente será una dirección diferente de su asociado de porque cada proceso puede asignar búferes en direcciones distintas.

**Sintaxis** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |**pBuffer** |Se trata de la dirección de un búfer obtenido de un comando de lectura o escritura.
| |**BufferHandle** |Se devuelve un identificador único para el búfer.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |La función se ha realizado correctamente.
| |**VD_E_PROTOCOL** |El conjunto de dispositivos virtual no está abierto actualmente.
| |**VD_E_INVALID** |PBuffer no es una dirección válida.
Notas del proceso que invoca la función GetBufferHandle es responsable de invocar ClientVirtualDevice::CompleteCommand una vez completada la transferencia de datos.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**Propósito** esta función se utiliza para obtener una dirección de búfer válido de un identificador de búfer obtenido de algún otro proceso. 

**Sintaxis** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |**dwBuffer** |Este es el identificador devuelto por ClientVirtualDeviceSet::GetBufferHandle.
| |**ppBuffer** |Esta es la dirección del búfer que es válido en el proceso actual.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |La función se ha realizado correctamente.
| |**VD_E_PROTOCOL** |El conjunto de dispositivos virtual no está abierto actualmente.
| |**VD_E_INVALID** |El ppBuffer es un identificador no válido.

**Comentarios** debe tener cuidado para comunicar correctamente los identificadores. Los identificadores son locales a un conjunto único de dispositivo virtual. Los procesos asociados compartir un identificador deben asegurarse de ese búfer identificadores se usan sólo en el ámbito del dispositivo virtual establecido del que se obtuvo originalmente el búfer.


