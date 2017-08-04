---
title: "Especificación de copia de seguridad de VDI, SQL Server en Linux | Documentos de Microsoft"
description: "Especificación de interfaz de dispositivo Virtual de copia de seguridad de SQL Server."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b0fec674c130732a159598797ce332070dd6242e
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>SQL Server en el cliente de Linux VDI especificación de SDK

Este documento tratan las interfaces proporcionadas por SQL Server en el SDK del cliente de dispositivo virtual (VDI) de la interfaz de Linux. Proveedores de software independientes (ISV) pueden usar el Virtual copia de seguridad de dispositivo aplicación interfaz de programación (API) para integrar SQL Server en sus productos. En general, VDI en Linux se comporta de forma similar a VDI en Windows con los cambios siguientes:

- Memoria compartida de Windows se convierte en la memoria compartida de POSIX.
- Los semáforos de Windows se convierten en POSIX semáforos.
- Tipos de Windows como HRESULT y DWORD se cambian a equivalentes de entero.
- Las interfaces COM se quitan y se reemplazan con un par de clases de C++.
- SQL Server en Linux no admite instancias con nombre, por lo que se han quitado las referencias al nombre de instancia. 
- La biblioteca compartida se implementa en libsqlvdi.so instalado en /opt/mssql/lib/libsqlvdi.so

Este documento es un anexo a **vbackup.chm** que detalla la especificación de VDI de Windows. Descargue el [Windows VDI especificación](http://www.microsoft.com/download/details.aspx?id=17282).

Revise también la solución de copia de seguridad de VDI de ejemplo en el [repositorio de GitHub de ejemplos de SQL Server](http://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux).

## <a name="user-permissions-setup"></a>Configuración de permisos de usuario

En Linux, primitivas POSIX son propiedad del usuario que crea ellos y su grupo de manera predeterminada. Para los objetos creados por SQL Server, estos será de forma predeterminada la propietaria del usuario mssql y el grupo de mssql. Para permitir el uso compartido entre SQL Server y el cliente VDI, se recomienda uno de los dos métodos siguientes:

1. Ejecute al cliente de VDI como el usuario mssql
   
   Ejecute el siguiente comando para cambiar a usuario mssql:
   
   ```bash
   sudo su mssql
   ```

2. Agregue el usuario mssql al grupo del vdiuser y la vdiuser al grupo mssql.
   
   Ejecute los comandos siguientes:

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   Reinicie el servidor a recoger nuevos grupos de SQL Server y vdiuser

## <a name="client-functions"></a>Funciones de cliente

En este capítulo se incluyen descripciones de cada una de las funciones de cliente. Las descripciones de incluyen la siguiente información:

- Propósito de la función
- Sintaxis de la función
- Lista de parámetros
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
| | **Nombre** | Esto identifica el conjunto de dispositivos virtuales. Se deben seguir las reglas de nombres utilizados por CreateFileMapping(). Cualquier carácter excepto con barra diagonal inversa (\) puede utilizarse. Se trata de una cadena de caracteres. Se recomienda un prefijo de la cadena con el nombre de producto o de empresa y el nombre de base de datos del usuario. |
| |**cfg** | Se trata de la configuración para el conjunto de dispositivos virtuales. Para obtener más información, consulte "Configuración" más adelante en este documento.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** | La función se ha realizado correctamente. |
| |**VD_E_NOTSUPPORTED** |Uno o varios de los campos en la configuración no era válido o no se admite en caso contrario. |
| |**VD_E_PROTOCOL** | El dispositivo virtual ya existe.

**Comentarios** crear el método debe llamarse una sola vez por cada operación de copia de seguridad o restauración. Después de invocar el método de cierre, el cliente puede volver a usar la interfaz para crear otro conjunto de dispositivos virtuales.

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**Propósito** esta función se utiliza para esperar a que el servidor configurar el conjunto de dispositivos virtuales.
**Sintaxis**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| | **tiempo de espera** | Este es el tiempo de espera en milisegundos. Usar infinito o un número entero negativo para evitar el tiempo de espera.
| | **cfg** | Tras la ejecución correcta, contiene la configuración seleccionada por el servidor. Para obtener más información, consulte "Configuración" más adelante en este documento.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** | Se devolvió la configuración.
| |**VD_E_ABORT** |Se invocó SignalAbort.
| |**VD_E_TIMEOUT** |La función agotó el tiempo de espera.

**Comentarios** esta función se bloquea en un estado de alerta. Después de la invocación correcta, se pueden abrir los dispositivos en el conjunto de dispositivos virtuales.


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**Propósito** esta función abre a uno de los dispositivos en el conjunto de dispositivos virtuales.
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
| |**VD_E_PROTOCOL** |  El conjunto no está en el estado de inicialización o este dispositivo concreto ya está abierta.
| |**VD_E_INVALID** |El nombre del dispositivo no es válido. No es uno de los nombres que se sabe que componen el conjunto.

**Comentarios** VD_E_OPEN puede devolverse sin problema. El cliente puede llamar a OpenDevice por medio de un bucle hasta que se devuelve este código.
Si se configura más de un dispositivo, por ejemplo  *n*  dispositivos, devolverá el conjunto de dispositivos virtuales  *n*  interfaces de dispositivo único.

El `GetConfiguration` función puede utilizarse para esperar hasta que se pueden abrir los dispositivos.
Si esta función no se realiza correctamente, se devuelve un valor null a través de la ppVirtualDevice.
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**Propósito** esta función se utiliza para obtener el siguiente comando en cola en un dispositivo. Cuando se solicita, esta función espera a que el comando siguiente.

**Sintaxis**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |**tiempo de espera** |Se trata de tiempo de espera, en milisegundos. Utilice INFINTE para esperar indefinidamente. Use 0 para sondear en busca de un comando. Si no hay ningún comando está actualmente disponible, se devuelve VD_E_TIMEOUT. Si se produce el tiempo de espera, el cliente decide la siguiente acción.
| |**Timeout** |Se trata de tiempo de espera, en milisegundos. Utilice INFINTE o un valor negativo para esperar indefinidamente. Use 0 para sondear en busca de un comando. Si no hay ningún comando está disponible antes de que expire el tiempo de espera, se devuelve VD_E_TIMEOUT. Si se produce el tiempo de espera, el cliente decide la siguiente acción.
| |**ppCmd** |Cuando un comando se devuelve correctamente, el parámetro devuelve la dirección de un comando para ejecutar. La memoria devuelta es de solo lectura. Cuando se completa el comando, este puntero se pasa a la rutina CompleteCommand. Para obtener más información acerca de cada comando, vea "Comandos" más adelante en este documento.
        
| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |Se capturó un comando.
| |**VD_E_CLOSE** |El dispositivo se ha cerrado el servidor.
| |**VD_E_TIMEOUT** |No hay ningún comando estaba disponible y el tiempo de espera expirado.
| |**VD_E_ABORT** |El cliente o el servidor ha utilizado el SignalAbort para forzar el cierre.

**Comentarios** VD_E_CLOSE cuando se devuelve, SQL Server ha cerrado el dispositivo. Esto forma parte del cierre normal. Una vez que se han cerrado todos los dispositivos, el cliente invoca ClientVirtualDeviceSet::Close para cerrar el conjunto de dispositivos virtuales.
Cuando esta rutina se debe bloquear para esperar un comando, el subproceso se deja en una condición de alerta.

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**Propósito** esta función se utiliza para notificar a SQL Server que ha terminado de un comando. Se debería devolver información de finalización adecuada para el comando. Para obtener más información, vea "Comandos" más adelante en este documento.

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
| |**pCmd** |Se trata de la dirección de un comando devuelto anteriormente desde ClientVirtualDevice::GetCommand.
| |**completionCode** |Se trata de un código de estado que indica el estado de finalización. Este parámetro se debe devolver para todos los comandos. El código devuelto debe ser adecuado para el comando que se está realizando. ERROR_SUCCESS se utiliza en todos los casos para denotar un comando ejecutado correctamente. Para obtener la lista completa de los posibles códigos, vea el archivo vdierror.h. Aparece una lista de códigos de estado típico para cada comando en "Comandos" más adelante en este documento.
| |**bytesTransferred** |Este es el número de bytes transferidos correctamente. Esto solo se devuelve para transferencia de datos de comandos de lectura y escritura.
| |**position** |Se trata de una respuesta al comando GetPosition solo.
        
| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |Se observó correctamente la finalización.
| |**VD_E_INVALID** |pCmd no era un comando activo.
| |**VD_E_ABORT** |Anulación se había señalado.
| |**VD_E_PROTOCOL** |El dispositivo no está abierto.

**Comentarios** ninguno

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**Propósito** esta función se utiliza para indicar que se debe producir una finalización anormal.

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

**Comentarios** en cualquier momento, el cliente puede optar por anular la operación de copia de seguridad o restauración. Esta rutina indica que deben dejar de todas las operaciones. El estado del conjunto de dispositivo virtual entra en un estado termina de forma anómala. Se devuelve ningún comando adicional en los dispositivos. Todos los comandos incompletas se completan automáticamente, devolver ERROR_OPERATION_ABORTED como un código de finalización. El cliente debe llamar a ClientVirtualDeviceSet::Close una vez que ha finalizado con seguridad cualquier uso pendiente de búferes que se ha proporcionado al cliente. Para obtener más información, vea "Terminación anómala" anteriormente en este documento.

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
| |**VD_E_PROTOCOL** |Se realizó ninguna acción porque no estaba abierto el conjunto de dispositivos virtuales.
| |**VD_E_OPEN** |Dispositivos eran permanece abiertos.

**Comentarios** la invocación de cierre es una declaración de cliente que se deben liberar todos los recursos usados por el conjunto de dispositivos virtuales. El cliente debe asegurarse de que todas las actividades implicadas en los búferes de datos y dispositivos virtuales se terminen antes de invocar el cierre. Todas las interfaces de dispositivo virtual devueltas OpenDevice dejan de cierre.
El cliente tiene permiso para emitir una llamada de creación en la interfaz de dispositivo virtual conjunto después de que se devuelva la llamada de cierre. Una de estas llamadas crearía un nuevo dispositivo virtual establecido para una operación de copia de seguridad o restauración posterior.
Si se llama a Close cuando uno o más dispositivos virtuales aún están abiertos, se devuelve VD_E_OPEN. En este caso, SignalAbort se internamente desencadena, para garantizar un cierre correcto si es posible. Libera los recursos VDI. El cliente debe esperar para obtener una indicación VD_E_CLOSE en cada dispositivo antes de invocar ClientVirtualDeviceSet::Close. Si el cliente sabe que el conjunto de dispositivo virtual ya está en un estado anómalo finaliza, no debe esperar una indicación de VD_E_CLOSE de GetCommand y puede invocar ClientVirtualDeviceSet::Close tan pronto como finaliza la actividad en los búferes compartidos.
Para obtener más información, vea "Terminación anómala" anteriormente en este documento.

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**Propósito** esta función abre el dispositivo virtual establecido en un cliente secundario. El cliente principal debe ya hayan usado crear y GetConfiguration para configurar el conjunto de dispositivos virtuales.

**Sintaxis** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |**setName** |Esto identifica el conjunto. Este nombre distingue mayúsculas de minúsculas y debe coincidir con el nombre utilizado por el cliente principal cuando invoca ClientVirtualDeviceSet::Create.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |La función se ha realizado correctamente.
| |**VD_E_PROTOCOL** |El conjunto de dispositivos virtuales no se ha creado, ya se ha abierto en este cliente o el dispositivo virtual conjunto no está listo para aceptar las solicitudes abiertas desde clientes secundarias.
| |**VD_E_ABORT** |La operación se va a anular.

**Comentarios** cuando se utiliza un modelo de proceso múltiple, el cliente principal es responsable de detectar terminación normal e irregulares de clientes secundarias.

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**Propósito** algunas aplicaciones pueden requerir más de un proceso para operar en los búferes devueltos por ClientVirtualDevice::GetCommand. En tales casos, el proceso que recibe el comando puede usar GetBufferHandle para obtener un identificador de proceso independientes que identifica el búfer. A continuación, se puede comunicar este identificador a cualquier otro proceso que también tiene el mismo abierto de dispositivo Virtual configurado. Ese proceso, a continuación, utilizaría ClientVirtualDeviceSet::MapBufferHandle para obtener la dirección del búfer. La dirección será probablemente una dirección diferente de su asociado de porque cada proceso puede asignar búferes en diferentes direcciones.

**Sintaxis** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| Parámetros | Argumento | Explicación
| ----- | ----- | ------ |
| |**pBuffer** |Se trata de la dirección de un búfer que se obtienen de un comando de lectura o escritura.
| |**BufferHandle** |Se devuelve un identificador único para el búfer.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |La función se ha realizado correctamente.
| |**VD_E_PROTOCOL** |El conjunto de dispositivos virtuales no está abierto actualmente.
| |**VD_E_INVALID** |El pBuffer no es una dirección válida.
Notas del proceso que invoca la función GetBufferHandle es responsable de invocar ClientVirtualDevice::CompleteCommand una vez completada la transferencia de datos.

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**Propósito** esta función se utiliza para obtener una dirección válida de búfer de identificador de búfer que se obtiene desde algún otro proceso. 

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
| |**ppBuffer** |Se trata de la dirección del búfer que es válido en el proceso actual.

| Valores devueltos | Argumento | Explicación
| ----- | ----- | ------ |
| |**NOERROR** |La función se ha realizado correctamente.
| |**VD_E_PROTOCOL** |El conjunto de dispositivos virtuales no está abierto actualmente.
| |**VD_E_INVALID** |El ppBuffer es un identificador no válido.

**Comentarios** debe tener cuidado para comunicar los controladores correctamente. Identificadores son locales a un conjunto único de dispositivo virtual. Los procesos de socios comerciales compartir un identificador deben asegurarse de dicho búfer identificadores se usan solo dentro del ámbito de la configuración del que se obtuvo originalmente el búfer del dispositivo virtual.



