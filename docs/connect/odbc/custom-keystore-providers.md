---
title: Los proveedores de almacén de claves personalizado | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
manager: jroth
author: MightyPen
ms.openlocfilehash: 84e729cd60a28ff8a58760bd3810ec538a327007
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800487"
---
# <a name="custom-keystore-providers"></a>Proveedores de almacén de claves personalizados
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Información general

La característica de cifrado de columna de SQL Server 2016 requiere que el cifrado columna claves de cifrado (ECEKs) almacenadas en el servidor se recuperados por el cliente y, a continuación, se descifran a claves de cifrado de columna (las CEK) para tener acceso a los datos almacenados en columnas cifradas. ECEKs se cifran mediante claves maestras de columna (CMK) y la seguridad de la CMK es importante para la seguridad del cifrado de columna. Por lo tanto, la CMK se debe almacenar en una ubicación segura; el propósito de un proveedor de almacén de claves de cifrado de columna es proporcionar una interfaz para permitir que el controlador ODBC acceder a ellos de forma segura almacenados CMK. Para los usuarios con su propio almacenamiento seguro, la interfaz del proveedor de almacén de claves personalizado proporciona un marco para implementar el acceso para proteger el almacenamiento de la CMK para el controlador ODBC, que, a continuación, se puede usar para realizar la CEK cifrado y descifrado.

Cada proveedor de almacén de claves contiene y administra uno o más CMK, que se identifica mediante rutas de acceso de claves: las cadenas de formato definido por el proveedor. Esto, junto con el algoritmo de cifrado también una cadena definida por el proveedor, puede utilizarse para realizar el cifrado de una CEK y el descifrado de una ECEK. El algoritmo, junto con ECEK y el nombre del proveedor, se almacenan en los metadatos de cifrado de la base de datos; consulte [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) y [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) para obtener más información. Por lo tanto, son las dos operaciones fundamentales de administración de claves:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

donde el `CEKeystoreProvider_name` se usa para identificar el proveedor de almacén de claves de cifrado de columna concreto (CEKeystoreProvider), y los demás argumentos se usan por el CEKeystoreProvider para cifrar o descifrar la CEK (E). El nombre y la ruta de acceso clave se proporcionan los metadatos de CMK, mientras que el algoritmo y el valor ECEK se proporcionan los metadatos de la CEK. Varios proveedores de almacén de claves pueden encontrarse junto con los proveedores integrados de forma predeterminada. Tras realizar una operación que requiere la CEK, el controlador usa los metadatos CMK para encontrar el proveedor de almacén de claves adecuado por su nombre y ejecuta su operación de descifrado, que puede expresarse como:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

Aunque el controlador no tiene necesidad cifran las CEK, una herramienta de administración de claves que deba hacerlo con el fin de implementar operaciones como la creación de CMK y giro; Para ello, realiza la operación inversa:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>Interfaz CEKeyStoreProvider

Este documento describe en detalle la interfaz CEKeyStoreProvider. Un proveedor de almacén de claves que implementa esta interfaz se puede usar el controlador ODBC de Microsoft para SQL Server. Los implementadores de CEKeyStoreProvider pueden usar a esta guía para desarrollar proveedores de almacén de claves personalizado puede usar el controlador.

Una biblioteca de proveedor de almacén de claves ("biblioteca de proveedor") es una biblioteca de vínculos dinámicos que se puede cargar el controlador ODBC y contiene uno o varios proveedores de almacén de claves. El símbolo `CEKeystoreProvider` debe exportarse en una biblioteca de proveedor, y ser la dirección de una matriz terminada en null de punteros a `CEKeystoreProvider` estructuras, uno para cada proveedor de almacén de claves dentro de la biblioteca.

Un `CEKeystoreProvider` estructura define los puntos de entrada de un proveedor de almacén de claves único:

```
typedef struct CEKeystoreProvider {
    wchar_t *Name;
    int (*Init)(CEKEYSTORECONTEXT *ctx, errFunc *onError);
    int (*Read)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int *len);
    int (*Write)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len);
    int (*DecryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *ecek,
                        unsigned short ecekLen,
                        unsigned char **cekOut,
                        unsigned short *cekLen);
    int (*EncryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *cek,
                        unsigned short cekLen,
                        unsigned char **ecekOut,
                        unsigned short *ecekLen);
    void (*Free)();
} CEKEYSTOREPROVIDER;
```

|Nombre de campo|Descripción|
|:--|:--|
|`Name`|El nombre del proveedor de almacén de claves. No debe ser igual que cualquier otro proveedor de almacén de claves se cargaron previamente por el controlador o está presente en esta biblioteca. Cadena de caracteres anchos* terminada en NULL.|
|`Init`|Función de inicialización. Si no se requiere una función de inicialización, este campo puede ser null.|
|`Read`|Proveedor de read, función. Puede ser null si no es necesario.|
|`Write`|Función de escritura de proveedor. Requerido si lectura no es null. Puede ser null si no es necesario.|
|`DecryptCEK`|Función ECEK descifrado. Esta función es la razón por la existencia de un proveedor de almacén de claves y no debe ser null.|
|`EncryptCEK`|Función de cifrado de la CEK. El controlador no llama a esta función, pero se proporciona para permitir el acceso mediante programación a la creación de ECEK las herramientas de administración de claves. Puede ser null si no es necesario.|
|`Free`|Función de finalización. Puede ser null si no es necesario.|

Gratis, con la excepción de las funciones de esta interfaz todos tienen un par de parámetros, **ctx** y **onError**. El primero identifica el contexto en el que se llama a la función, mientras que se usa para notificar errores. Consulte [contextos](#context-association) y [Error Handling](#error-handling) a continuación para obtener más información.

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
Nombre de marcador de posición para una función de inicialización definido por el proveedor. El controlador llama a esta función una vez, después de un proveedor se ha cargado, pero antes del primer tiempo lo necesite para realizar el descifrado de ECEK o Read()/Write() las solicitudes. Utilice esta función para realizar cualquier inicialización que necesita. 

|Argumento|Descripción|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de notificación de error.|
|`Return Value`|Devolver distinto de cero para indicar el éxito o cero para indicar el error.|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

Nombre de marcador de posición para una función definida por el proveedor de comunicación. El controlador llama a esta función cuando la aplicación solicita para leer datos de un (anteriormente escrito-a) proveedor mediante el atributo de conexión SQL_COPT_SS_CEKEYSTOREDATA, lo que permite la aplicación lea datos arbitrarios desde el proveedor. Consulte [comunicarse con los proveedores de almacén de claves](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) para obtener más información.

|Argumento|Descripción|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de notificación de error.|
|`data`|[Salida] Puntero a un búfer en el que el proveedor escribe datos en la aplicación se lee. Esto corresponde al campo de datos de la estructura CEKEYSTOREDATA.|
|`len`|[Entrada] Puntero a un valor de longitud. Tras la entrada, se trata de la longitud máxima del búfer de datos y el proveedor no debe escribir más de * len bytes a él. Tras la devolución, debe actualizar el proveedor * len con el número de bytes escritos realmente.|
|`Return Value`|Devolver distinto de cero para indicar el éxito o cero para indicar el error.|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
Nombre de marcador de posición para una función definida por el proveedor de comunicación. El controlador llama a esta función cuando la aplicación solicita para escribir datos en un proveedor mediante el atributo de conexión SQL_COPT_SS_CEKEYSTOREDATA, lo que permite la aplicación escribir datos arbitrarios en el proveedor. Consulte [comunicarse con los proveedores de almacén de claves](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) para obtener más información.

|Argumento|Descripción|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de notificación de error.|
|`data`|[Entrada] Puntero a un búfer que contiene los datos del proveedor al leer. Esto corresponde al campo de datos de la estructura CEKEYSTOREDATA. El proveedor no debe leer más de bytes de longitud de este búfer.|
|`len`|[Entrada] El número de bytes disponibles en los datos. Esto corresponde al campo de la estructura CEKEYSTOREDATA dataSize.|
|`Return Value`|Devolver distinto de cero para indicar el éxito o cero para indicar el error.|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
Nombre de marcador de posición para una función definida por el proveedor de descifrado de ECEK. El controlador llama a esta función para descifrar un cifrado por una CMK asociada a este proveedor en una CEK de ECEK.

|Argumento|Descripción|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de notificación de error.|
|`keyPath`|[Entrada] El valor de la [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) atributo de metadatos para la CMK ECEK determinado al que hace referencia. Cadena de caracteres anchos* terminada en NULL. Esto está pensado para identificar una CMK controlada por este proveedor.|
|`alg`|[Entrada] El valor de la [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) atributo de metadatos para ECEK determinado. Cadena de caracteres anchos* terminada en NULL. Esto está pensado para identificar el algoritmo de cifrado usado para cifrar el ECEK determinado.|
|`ecek`|[Entrada] Puntero a la que se va a descifrar ECEK.|
|`ecekLen`|[Entrada] Longitud de ECEK.|
|`cekOut`|[Salida] El proveedor deberá asignar memoria para ECEK descifrado y escribir su dirección en el puntero apuntado a cekOut. Debe ser posible liberar este bloque de memoria utilizando la [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) o función (Linux/Mac) gratis. Si no hay memoria se ha asignado debido a un error o en caso contrario, el proveedor debe establecer * cekOut a un puntero nulo.|
|`cekLen`|[Salida] El proveedor deberá escribir en la dirección cekLen apuntada a la longitud de ECEK descifrado que se ha escrito para ** cekOut.|
|`Return Value`|Devolver distinto de cero para indicar el éxito o cero para indicar el error.|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
Nombre de marcador de posición para una función definida por el proveedor de cifrado de CEK. El controlador no llame a esta función ni exponer su funcionalidad a través de la interfaz ODBC, pero se proporciona para permitir el acceso mediante programación a la creación de ECEK las herramientas de administración de claves.

|Argumento|Descripción|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de notificación de error.|
|`keyPath`|[Entrada] El valor de la [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) atributo de metadatos para la CMK ECEK determinado al que hace referencia. Cadena de caracteres anchos* terminada en NULL. Esto está pensado para identificar una CMK controlada por este proveedor.|
|`alg`|[Entrada] El valor de la [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) atributo de metadatos para ECEK determinado. Cadena de caracteres anchos* terminada en NULL. Esto está pensado para identificar el algoritmo de cifrado usado para cifrar el ECEK determinado.|
|`cek`|[Entrada] Puntero a la CEK se cifren.|
|`cekLen`|[Entrada] Longitud de la CEK.|
|`ecekOut`|[Salida] El proveedor deberá asignar memoria para la CEK cifrada y escribir su dirección en el puntero apuntado a ecekOut. Debe ser posible liberar este bloque de memoria utilizando la [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) o función (Linux/Mac) gratis. Si no hay memoria se ha asignado debido a un error o en caso contrario, el proveedor debe establecer * ecekOut a un puntero nulo.|
|`ecekLen`|[Salida] El proveedor deberá escribir en la dirección ecekLen apuntada a la longitud de la CEK cifrada que se ha escrito para ** ecekOut.|
|`Return Value`|Devolver distinto de cero para indicar el éxito o cero para indicar el error.|

```
void (*Free)();
```
Nombre de marcador de posición para una función definida por el proveedor de terminación. El controlador puede llamar a esta función tras la finalización normal del proceso.

> [!NOTE]
> *Cadenas de caracteres anchos son caracteres de 2 bytes (UTF-16) debido a cómo SQL Server almacena.*


### <a name="error-handling"></a>Tratamiento de errores

Como es posible que se producen errores durante el procesamiento de un proveedor, se proporciona un mecanismo para permitir que se informe de errores hasta que el controlador con más detalle que un éxito/error booleano. Muchas de las funciones tienen un par de parámetros, **ctx** y **onError**, que se usan juntos para este propósito, además del valor devuelto correctos o con errores.

El **ctx** parámetro identifica el contexto en el que se produce una operación de proveedor.

El **onError** parámetro señala a una función de informes de errores, con el prototipo siguiente:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|Argumento|Descripción|
|:--|:--|
|`ctx`|[Entrada] Para notificar el error en el contexto.|
|`msg`|[Entrada] El mensaje de error para el informe. Cadena de caracteres anchos terminada en NULL. Para permitir que se presente la información con parámetros, esta cadena puede contener secuencias de formato para insertar el formato aceptado por el [FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage) función. Funcionalidad extendida se puede especificar mediante este parámetro, tal como se describe a continuación.|
|…|[Entrada] Parámetros adicionales variadic ajustar especificadores de formato de mensaje, según corresponda.|

Para notificar cuando se ha producido un error, el onError de llamadas de proveedor, proporcionando el parámetro de contexto se pasa a la función de proveedor por el controlador y un mensaje de error con parámetros adicionales opcionales para dar formato. El proveedor puede llamar a esta función varias veces para enviar varios mensajes de error consecutivas en la invocación de una función de proveedor. Por ejemplo:

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


El `msg` parámetro normalmente es una cadena de caracteres anchos, pero las extensiones adicionales están disponibles:

Pueden utilizarse mediante uno de los valores predefinidos especiales con la macro IDS_MSG, mensajes de error genéricos existentes y en un formulario localizado en el controlador. Por ejemplo, si un proveedor no puede asignar memoria, el `IDS_S1_001` se puede usar el mensaje "Error de asignación de memoria":

`onError(ctx, IDS_MSG(IDS_S1_001));`

El error ser reconocido por el controlador, la función de proveedor debe devolver un error. Cuando esto se realiza en el contexto de una operación de ODBC, los errores registrados estará accesibles en el identificador de instrucción o la conexión a través del mecanismo de diagnóstico estándar de ODBC (`SQLError`, `SQLGetDiagRec`, y `SQLGetDiagField`).


### <a name="context-association"></a>Asociación de contexto

El `CEKEYSTORECONTEXT` estructura, además de proporcionar contexto para la devolución de llamada de error, también puede utilizarse para determinar el contexto ODBC en el que se ejecuta una operación de proveedor. Esto permite a un proveedor asociar los datos a cada uno de estos contextos, por ejemplo, para implementar la configuración de cada conexión. Para este propósito, la estructura contiene punteros opacos 3 correspondiente al contexto de entorno, la conexión y la instrucción:

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```

|Campo|Descripción|
|:--|:--|
|`envCtx`|Contexto de entorno.|
|`dbcCtx`|Contexto de conexión.|
|`stmtCtx`|Contexto de la instrucción.|

Cada uno de estos contextos es un valor opaco que, mientras no es el mismo que el controlador ODBC correspondiente, se puede usar como un identificador único para el identificador: si controlar *X* está asociado con el valor de contexto *Y*, a continuación, No hay otros identificadores entorno, conexión o la instrucción que existen simultáneamente al mismo tiempo como *X* tendrá un valor de contexto de *Y*, y no se asociará ningún otro valor de contexto controlar *X*. Si está llevando a cabo la operación de proveedor no tiene un contexto de controlador determinado (por ejemplo, llamadas de SQLSetConnectAttr para cargar y configurar los proveedores, en el que no hay ningún identificador de instrucción) el correspondiente valor de contexto de la estructura es null.


## <a name="example"></a>Ejemplo

### <a name="keystore-provider"></a>Proveedor de almacén de claves

El código siguiente es un ejemplo de una implementación de proveedor de almacén de claves mínima.

```
/* Custom Keystore Provider Example

Windows:   compile with cl MyKSP.c /LD /MD /link /out:MyKSP.dll
Linux/Mac: compile with gcc -fshort-wchar -fPIC -o MyKSP.so -shared MyKSP.c

 */

#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#endif

#include <stdlib.h>
#include <sqltypes.h>
#include "msodbcsql.h"
#include <sql.h>
#include <sqlext.h>

int __stdcall KeystoreInit(CEKEYSTORECONTEXT *ctx, errFunc *onError) {
    printf("KSP Init() function called\n");
    return 1;
}

static unsigned char *g_encryptKey;
static unsigned int g_encryptKeyLen;

int __stdcall KeystoreWrite(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len) {
    printf("KSP Write() function called (%d bytes)\n", len);
    if (len) {
        if (g_encryptKey)
            free(g_encryptKey);
        g_encryptKey = malloc(len);
        if (!g_encryptKey) {
            onError(ctx, L"Memory Allocation Error");
            return 0;
        }
        memcpy(g_encryptKey, data, len);
        g_encryptKeyLen = len;
    }
    return 1;
}

// Very simple "encryption" scheme - rotating XOR with the key
int __stdcall KeystoreDecrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg,
    unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen) {
    unsigned int i;
    printf("KSP Decrypt() function called (keypath=%S alg=%S ecekLen=%u)\n", keyPath, alg, ecekLen);
    if (wcscmp(keyPath, L"TheOneAndOnlyKey")) {
        onError(ctx, L"Invalid key path");
        return 0;
    }
    if (wcscmp(alg, L"none")) {
        onError(ctx, L"Invalid algorithm");
        return 0;
    }
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
#ifndef _WIN32
    *cekOut = malloc(ecekLen);
#else
    *cekOut = LocalAlloc(LMEM_FIXED, ecekLen);
#endif
    if (!*cekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *cekLen = ecekLen;
    for (i = 0; i < ecekLen; i++)
        (*cekOut)[i] = ecek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

// Note that in the provider interface, this function would be referenced via the CEKEYSTOREPROVIDER
// structure. However, that does not preclude keystore providers from exporting their own functions,
// as illustrated by this example where the encryption is performed via a separate function (with a
// different prototype than the one in the KSP interface.)
#ifdef _WIN32
__declspec(dllexport)
#endif
int KeystoreEncrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError,
    unsigned char *cek, unsigned short cekLen,
    unsigned char **ecekOut, unsigned short *ecekLen) {
    unsigned int i;
    printf("KSP Encrypt() function called (cekLen=%u)\n", cekLen);
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
    *ecekOut = malloc(cekLen);
    if (!*ecekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *ecekLen = cekLen;
    for (i = 0; i < cekLen; i++)
        (*ecekOut)[i] = cek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

CEKEYSTOREPROVIDER MyCustomKSPName_desc = {
    L"MyCustomKSPName",
    KeystoreInit,
    0,
    KeystoreWrite,
    KeystoreDecrypt,
    0
};

#ifdef _WIN32
__declspec(dllexport)
#endif
CEKEYSTOREPROVIDER *CEKeystoreProvider[] = {
    &MyCustomKSPName_desc,
    0
};
```

### <a name="odbc-application"></a>Aplicación de ODBC

El código siguiente es una aplicación de demostración que usa el proveedor de almacén de claves anterior. Al ejecutarlo, asegúrese de que la biblioteca del proveedor está en el mismo directorio que el archivo binario de la aplicación, y que especifica la cadena de conexión (o especifica un DSN que contiene) el `ColumnEncryption=Enabled` configuración.

```
/*
 Example application for demonstration of custom keystore provider usage

Windows:   compile with cl /MD kspapp.c /link odbc32.lib
Linux/Mac: compile with gcc -o kspapp -fshort-wchar kspapp.c -lodbc -ldl
 
 usage: kspapp connstr

 */

#define KSPNAME L"MyCustomKSPName"
#define PROV_ENCRYPT_KEY "JHKCWYT06N3RG98J0MBLG4E3"

#include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#include <dlfcn.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include "msodbcsql.h"

/* Convenience functions */

int checkRC(SQLRETURN rc, char *msg, int ret, SQLHANDLE h, SQLSMALLINT ht) {
    if (rc == SQL_ERROR) {
        fprintf(stderr, "Error occurred upon %s\n", msg);
        if (h) {
            SQLSMALLINT i = 0;
            SQLSMALLINT outlen = 0;
            char errmsg[1024];
            while ((rc = SQLGetDiagField(
                ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
                || rc == SQL_SUCCESS_WITH_INFO) {
                fprintf(stderr, "Err#%d: %s\n", i, errmsg);
            }
        }
        if (ret)
            exit(ret);
        return 0;
    }
    else if (rc == SQL_SUCCESS_WITH_INFO && h) {
        SQLSMALLINT i = 0;
        SQLSMALLINT outlen = 0;
        char errmsg[1024];
        printf("Success with info for %s:\n", msg);
        while ((rc = SQLGetDiagField(
            ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
            || rc == SQL_SUCCESS_WITH_INFO) {
            fprintf(stderr, "Msg#%d: %s\n", i, errmsg);
        }
    }
    return 1;
}

void postKspError(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...) {
    if (msg > (wchar_t*)65535)
        wprintf(L"Provider emitted message: %s\n", msg);
    else
        wprintf(L"Provider emitted message ID %d\n", msg);
}

int main(int argc, char **argv) {
    char sqlbuf[1024];
    SQLHENV env;
    SQLHDBC dbc;
    SQLHSTMT stmt;
    SQLRETURN rc;
    unsigned char CEK[32];
    unsigned char *ECEK;
    unsigned short ECEKlen;
#ifdef _WIN32
    HMODULE hProvLib;
#else
    void *hProvLib;
#endif
    CEKEYSTORECONTEXT ctx = {0};
    CEKEYSTOREPROVIDER **ppKsp, *pKsp;
    int(__stdcall *pEncryptCEK)(CEKEYSTORECONTEXT *, errFunc *, unsigned char *, unsigned short, unsigned char **, unsigned short *);
    int i;
    if (argc < 2) {
        fprintf(stderr, "usage: kspapp connstr\n");
        return 1;
    }

    /* Load the provider library */
#ifdef _WIN32
    if (!(hProvLib = LoadLibrary("MyKSP.dll"))) {
#else
    if (!(hProvLib = dlopen("./MyKSP.so", RTLD_NOW))) {
#endif
        fprintf(stderr, "Error loading KSP library\n");
        return 2;
    }
#ifdef _WIN32
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)GetProcAddress(hProvLib, "CEKeystoreProvider"))) {
#else
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)dlsym(hProvLib, "CEKeystoreProvider"))) {
#endif
        fprintf(stderr, "The export CEKeystoreProvider was not found in the KSP library\n");
        return 3;
    }
    while (pKsp = *ppKsp++) {
        if (!memcmp(KSPNAME, pKsp->Name, sizeof(KSPNAME)))
            goto FoundProv;
    }
    fprintf(stderr, "Could not find provider in the library\n");
    return 4;
FoundProv:
    if (pKsp->Init && !pKsp->Init(&ctx, postKspError)) {
        fprintf(stderr, "Could not initialize provider\n");
        return 5;
    }
#ifdef _WIN32
    if (!(pEncryptCEK = (LPVOID)GetProcAddress(hProvLib, "KeystoreEncrypt"))) {
#else
    if (!(pEncryptCEK = dlsym(hProvLib, "KeystoreEncrypt"))) {
#endif
        fprintf(stderr, "The export KeystoreEncrypt was not found in the KSP library\n");
        return 6;
    }
    if (!pKsp->Write) {
        fprintf(stderr, "Provider does not support configuration\n");
        return 7;
    }

    /* Configure the provider with the key */
    if (!pKsp->Write(&ctx, postKspError, PROV_ENCRYPT_KEY, strlen(PROV_ENCRYPT_KEY))) {
        fprintf(stderr, "Error writing to KSP\n");
        return 8;
    }

    /* Generate a CEK and encrypt it with the provider */
    srand(time(0) ^ getpid());
    for (i = 0; i < sizeof(CEK); i++)
        CEK[i] = rand();

    if (!pEncryptCEK(&ctx, postKspError, CEK, sizeof(CEK), &ECEK, &ECEKlen)) {
        fprintf(stderr, "Error encrypting CEK\n");
        return 9;
    }

    /* Connect to Server */
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &env);
    checkRC(rc, "allocating environment handle", 2, 0, 0);
    rc = SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);
    checkRC(rc, "setting ODBC version to 3.0", 3, env, SQL_HANDLE_ENV);
    rc = SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc);
    checkRC(rc, "allocating connection handle", 4, env, SQL_HANDLE_ENV);
    rc = SQLDriverConnect(dbc, 0, argv[1], strlen(argv[1]), NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    checkRC(rc, "connecting to data source", 5, dbc, SQL_HANDLE_DBC);
    rc = SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt);
    checkRC(rc, "allocating statement handle", 6, dbc, SQL_HANDLE_DBC);

    /* Create a CMK definition on the server */
    {
        static char cmkSql[] = "CREATE COLUMN MASTER KEY CustomCMK WITH ("
            "KEY_STORE_PROVIDER_NAME = 'MyCustomKSPName',"
            "KEY_PATH = 'TheOneAndOnlyKey')";
        printf("Create CMK: %s\n", cmkSql);
        SQLExecDirect(stmt, cmkSql, SQL_NTS);
    }

    /* Create a CEK definition on the server */
    {
        const char cekSqlBefore[] = "CREATE COLUMN ENCRYPTION KEY CustomCEK WITH VALUES ("
            "COLUMN_MASTER_KEY = CustomCMK,"
            "ALGORITHM = 'none',"
            "ENCRYPTED_VALUE = 0x";
        char *cekSql = malloc(sizeof(cekSqlBefore) + 2 * ECEKlen + 2); /* 1 for ')', 1 for null terminator */
        strcpy(cekSql, cekSqlBefore);
        for (i = 0; i < ECEKlen; i++)
            sprintf(cekSql + sizeof(cekSqlBefore) - 1 + 2 * i, "%02x", ECEK[i]);
        strcat(cekSql, ")");
        printf("Create CEK: %s\n", cekSql);
        SQLExecDirect(stmt, cekSql, SQL_NTS);
        free(cekSql);
#ifdef _WIN32
        LocalFree(ECEK);
#else
        free(ECEK);
#endif
    }

#ifdef _WIN32
    FreeLibrary(hProvLib);
#else
    dlclose(hProvLib);
#endif

    /* Create a table with encrypted columns */
    {
        static char *tableSql = "CREATE TABLE CustomKSPTestTable ("
            "c1 int,"
            "c2 varchar(255) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CustomCEK, ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'))";
        printf("Create table: %s\n", tableSql);
        SQLExecDirect(stmt, tableSql, SQL_NTS);
    }

    /* Load provider into the ODBC Driver and configure it */
    {
        unsigned char ksd[sizeof(CEKEYSTOREDATA) + sizeof(PROV_ENCRYPT_KEY) - 1];
        CEKEYSTOREDATA *pKsd = (CEKEYSTOREDATA*)ksd;
        pKsd->name = L"MyCustomKSPName";
        pKsd->dataSize = sizeof(PROV_ENCRYPT_KEY) - 1;
        memcpy(pKsd->data, PROV_ENCRYPT_KEY, sizeof(PROV_ENCRYPT_KEY) - 1);
#ifdef _WIN32
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "MyKSP.dll", SQL_NTS);
#else
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "./MyKSP.so", SQL_NTS);
#endif
        checkRC(rc, "Loading KSP into ODBC Driver", 7, dbc, SQL_HANDLE_DBC);
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREDATA, (SQLPOINTER)pKsd, SQL_IS_POINTER);
        checkRC(rc, "Configuring the KSP", 7, dbc, SQL_HANDLE_DBC);
    }

    /* Insert some data */
    {
        int c1;
        char c2[256];
        rc = SQLBindParameter(stmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 0, 0, &c1, 0, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        rc = SQLBindParameter(stmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 255, 0, c2, 255, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        for (i = 0; i < 10; i++) {
            c1 = i * 10 + i + 1;
            sprintf(c2, "Sample data %d for column 2", i);
            rc = SQLExecDirect(stmt, "INSERT INTO CustomKSPTestTable (c1, c2) values (?, ?)", SQL_NTS);
            checkRC(rc, "Inserting rows query", 10, stmt, SQL_HANDLE_STMT);
        }
        printf("(Encrypted) data has been inserted into the [CustomKSPTestTable]. You may inspect the data now.\n"
            "Press Enter to continue...\n");
        getchar();
    }

    /* Retrieve the data */
    {
        int c1;
        char c2[256];
        rc = SQLBindCol(stmt, 1, SQL_C_LONG, &c1, 0, 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLBindCol(stmt, 2, SQL_C_CHAR, c2, sizeof(c2), 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLExecDirect(stmt, "SELECT c1, c2 FROM CustomKSPTestTable", SQL_NTS);
        checkRC(rc, "Retrieving rows query", 12, stmt, SQL_HANDLE_STMT);
        while (SQL_SUCCESS == (rc = SQLFetch(stmt)))
            printf("Retrieved data: c1=%d c2=%s\n", c1, c2);
        SQLFreeStmt(stmt, SQL_CLOSE);
        printf("Press Enter to clean up and exit...\n");
        getchar();
    }

    /* Clean up */
    {
        SQLExecDirect(stmt, "DROP TABLE CustomKSPTestTable", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN ENCRYPTION KEY CustomCEK", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN MASTER KEY CustomCMK", SQL_NTS);
        printf("Removed table, CEK, and CMK\n");
    }
    SQLDisconnect(dbc);
    SQLFreeHandle(SQL_HANDLE_DBC, dbc);
    SQLFreeHandle(SQL_HANDLE_ENV, env);
    return 0;
}

```

## <a name="see-also"></a>Consulte también

[Uso de Always Encrypted con el controlador ODBC](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
