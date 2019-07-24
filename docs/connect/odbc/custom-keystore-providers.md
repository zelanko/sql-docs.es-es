---
title: Proveedores de almacén de claves personalizado | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: 0cf2946517be732094d01ff9889faf080a36e85b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006500"
---
# <a name="custom-keystore-providers"></a>Proveedores de almacén de claves personalizados
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Información general

La característica de cifrado de columnas de SQL Server 2016 requiere que el cliente recupere las claves de cifrado de columnas cifradas (ECEKs) que se almacenan en el servidor y que, a continuación, se descifren en las claves de cifrado de columnas (las CEK) para tener acceso a los datos almacenados en columnas cifradas. ECEKs se cifran mediante claves maestras de columna (CMK) y la seguridad de CMK es importante para la seguridad del cifrado de columnas. Por lo tanto, el CMK debe almacenarse en una ubicación segura. el propósito de un proveedor de almacén de claves de cifrado de columnas es proporcionar una interfaz para permitir que el controlador ODBC tenga acceso a estos CMK almacenados de forma segura. Para los usuarios con su propio almacenamiento seguro, la interfaz del proveedor de almacén de claves personalizado proporciona un marco para implementar el acceso al almacenamiento seguro de CMK para el controlador ODBC, que se puede usar para realizar el cifrado y descifrado de CEK.

Cada proveedor de almacén de claves contiene y administra uno o más CMK, que se identifican mediante rutas de acceso clave: cadenas de un formato definido por el proveedor. Esto, junto con el algoritmo de cifrado, también una cadena definida por el proveedor, se puede usar para realizar el cifrado de un CEK y el descifrado de un ECEK. El algoritmo, junto con ECEK y el nombre del proveedor, se almacenan en los metadatos de cifrado de la base de datos; vea [crear clave maestra de columna](../../t-sql/statements/create-column-master-key-transact-sql.md) y [crear clave](../../t-sql/statements/create-column-encryption-key-transact-sql.md) de cifrado de columna para obtener más información. Por lo tanto, las dos operaciones fundamentales de administración de claves son:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

`CEKeystoreProvider_name` donde se usa para identificar el proveedor de almacén de claves de cifrado de columnas específico (CEKeystoreProvider), y el CEKeystoreProvider usa los otros argumentos para cifrar o descifrar el (E) CEK. Los metadatos de CMK proporcionan el nombre y la ruta de rutas, mientras que los metadatos de CEK proporcionan el algoritmo y el valor ECEK. Pueden estar presentes varios proveedores de almacén de claves junto con los proveedores integrados predeterminados. Tras realizar una operación que requiere CEK, el controlador usa los metadatos de CMK para buscar el proveedor de almacén de claves adecuado por nombre y ejecuta su operación de descifrado, que se puede expresar de la siguiente manera:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

Aunque el controlador no tiene necesidad de cifrar las CEK, es posible que una herramienta de administración de claves tenga que hacerlo para implementar operaciones como la creación y la rotación de CMK. Esto requiere realizar la operación inversa:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>Interfaz CEKeyStoreProvider

En este documento se describe en detalle la interfaz CEKeyStoreProvider. El Microsoft ODBC Driver for SQL Server puede usar un proveedor de almacén de claves que implemente esta interfaz. Los implementadores de CEKeyStoreProvider pueden utilizar esta guía para desarrollar proveedores de almacén de claves personalizados que pueda usar el controlador.

Una biblioteca de proveedores de almacén de claves ("biblioteca de proveedores") es una biblioteca de vínculos dinámicos que puede cargar el controlador ODBC y contiene uno o más proveedores de almacén de claves. La biblioteca `CEKeystoreProvider` del proveedor debe exportar el símbolo y ser la dirección de una matriz terminada en NULL de punteros a `CEKeystoreProvider` estructuras, una para cada proveedor de almacén de claves dentro de la biblioteca.

Una `CEKeystoreProvider` estructura define los puntos de entrada de un único proveedor de almacén de claves:

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
|`Name`|Nombre del proveedor de almacén de claves. No debe ser igual que cualquier otro proveedor de almacén de claves cargado previamente por el controlador o presente en esta biblioteca. Cadena de caracteres anchos* terminada en NULL.|
|`Init`|Función de inicialización. Si no se requiere una función de inicialización, este campo puede ser null.|
|`Read`|Función read del proveedor. Puede ser null si no es necesario.|
|`Write`|Función de escritura de proveedor. Obligatorio si Read no es NULL. Puede ser null si no es necesario.|
|`DecryptCEK`|Función de descifrado de ECEK. Esta función es la razón por la existencia de un proveedor de almacén de claves y no debe ser null.|
|`EncryptCEK`|Función de cifrado CEK. El controlador no llama a esta función, pero se proporciona para permitir el acceso mediante programación a la creación de ECEK mediante las herramientas de administración de claves. Puede ser null si no es necesario.|
|`Free`|Función de terminación. Puede ser null si no es necesario.|

Con la excepción de Free, todas las funciones de esta interfaz tienen un par de parámetros, **CTX** y **OnError**. El primero identifica el contexto en el que se llama a la función, mientras que el último se usa para informar de errores. Vea [contextos](#context-association) y [control de errores](#error-handling) a continuación para obtener más información.

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
Nombre del marcador de posición para una función de inicialización definida por el proveedor. El controlador llama a esta función una vez, después de que se haya cargado un proveedor, pero antes de la primera vez que lo necesita para realizar las solicitudes de descifrado ECEK o Read ()/Write (). Utilice esta función para realizar cualquier inicialización que necesite. 

|Argumento|Descripción|
|:--|:--|
|`ctx`|Entradas Contexto de la operación.|
|`onError`|Entradas Función de generación de informes de errores.|
|`Return Value`|Devuelve un valor distinto de cero para indicar que se ha realizado correctamente, o cero para indicar un error.|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

Nombre del marcador de posición para una función de comunicación definida por el proveedor. El controlador llama a esta función cuando la aplicación solicita leer datos de un proveedor (previamente escrito) mediante el atributo de conexión SQL_COPT_SS_CEKEYSTOREDATA, lo que permite a la aplicación leer datos arbitrarios del proveedor. Consulte [comunicación con proveedores de almacén de claves](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) para obtener más información.

|Argumento|Descripción|
|:--|:--|
|`ctx`|Entradas Contexto de la operación.|
|`onError`|Entradas Función de generación de informes de errores.|
|`data`|Genere Puntero a un búfer en el que el proveedor escribe los datos que va a leer la aplicación. Esto corresponde al campo de datos de la estructura CEKEYSTOREDATA.|
|`len`|Inout Puntero a un valor de longitud; en la entrada, esta es la longitud máxima del búfer de datos y el proveedor no debe escribir más de * Len bytes. Cuando se devuelve, el proveedor debe actualizar * Len con el número de bytes escritos realmente.|
|`Return Value`|Devuelve un valor distinto de cero para indicar que se ha realizado correctamente, o cero para indicar un error.|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
Nombre del marcador de posición para una función de comunicación definida por el proveedor. El controlador llama a esta función cuando la aplicación solicita escribir datos en un proveedor mediante el atributo de conexión SQL_COPT_SS_CEKEYSTOREDATA, lo que permite que la aplicación escriba datos arbitrarios en el proveedor. Consulte [comunicación con proveedores de almacén de claves](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) para obtener más información.

|Argumento|Descripción|
|:--|:--|
|`ctx`|Entradas Contexto de la operación.|
|`onError`|Entradas Función de generación de informes de errores.|
|`data`|Entradas Puntero a un búfer que contiene los datos que el proveedor va a leer. Esto corresponde al campo de datos de la estructura CEKEYSTOREDATA. El proveedor no debe leer más de Len bytes de este búfer.|
|`len`|Entradas Número de bytes disponibles en los datos. Esto corresponde al campo Datasize de la estructura CEKEYSTOREDATA.|
|`Return Value`|Devuelve un valor distinto de cero para indicar que se ha realizado correctamente, o cero para indicar un error.|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
Nombre del marcador de posición para una función de descifrado de ECEK definida por el proveedor. El controlador llama a esta función para descifrar un ECEK cifrado por un CMK asociado a este proveedor en un CEK.

|Argumento|Descripción|
|:--|:--|
|`ctx`|Entradas Contexto de la operación.|
|`onError`|Entradas Función de generación de informes de errores.|
|`keyPath`|Entradas El valor del atributo de metadatos [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) para el CMK al que hace referencia el ECEK determinado. Cadena de caracteres anchos* terminada en NULL. Esto está pensado para identificar un CMK controlado por este proveedor.|
|`alg`|Entradas El valor del atributo de metadatos del [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) para el ECEK especificado. Cadena de caracteres anchos* terminada en NULL. Esto está pensado para identificar el algoritmo de cifrado utilizado para cifrar el ECEK determinado.|
|`ecek`|Entradas Puntero al ECEK que se va a descifrar.|
|`ecekLen`|Entradas Longitud de ECEK.|
|`cekOut`|Genere El proveedor debe asignar memoria para los ECEK descifrados y escribir su dirección en el puntero al que apunta cekOut. Debe ser posible liberar este bloque de memoria mediante la función [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) o Free (Linux/Mac). Si no se asignó ninguna memoria debido a un error o de lo contrario, el proveedor debe establecer * cekOut en un puntero nulo.|
|`cekLen`|Genere El proveedor debe escribir en la dirección a la que apunta cekLen la longitud del ECEK descifrado que ha escrito en * * cekOut.|
|`Return Value`|Devuelve un valor distinto de cero para indicar que se ha realizado correctamente, o cero para indicar un error.|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
Nombre del marcador de posición para una función de cifrado CEK definida por el proveedor. El controlador no llama a esta función ni expone su funcionalidad a través de la interfaz ODBC, pero se proporciona para permitir el acceso mediante programación a la creación de ECEK mediante las herramientas de administración de claves.

|Argumento|Descripción|
|:--|:--|
|`ctx`|Entradas Contexto de la operación.|
|`onError`|Entradas Función de generación de informes de errores.|
|`keyPath`|Entradas El valor del atributo de metadatos [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) para el CMK al que hace referencia el ECEK determinado. Cadena de caracteres anchos* terminada en NULL. Esto está pensado para identificar un CMK controlado por este proveedor.|
|`alg`|Entradas El valor del atributo de metadatos del [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) para el ECEK especificado. Cadena de caracteres anchos* terminada en NULL. Esto está pensado para identificar el algoritmo de cifrado utilizado para cifrar el ECEK determinado.|
|`cek`|Entradas Puntero al CEK que se va a cifrar.|
|`cekLen`|Entradas Longitud de CEK.|
|`ecekOut`|Genere El proveedor debe asignar memoria para el CEK cifrado y escribir su dirección en el puntero al que apunta ecekOut. Debe ser posible liberar este bloque de memoria mediante la función [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) o Free (Linux/Mac). Si no se asignó ninguna memoria debido a un error o de lo contrario, el proveedor debe establecer * ecekOut en un puntero nulo.|
|`ecekLen`|Genere El proveedor debe escribir en la dirección a la que apunta ecekLen la longitud del CEK cifrado que ha escrito en * * ecekOut.|
|`Return Value`|Devuelve un valor distinto de cero para indicar que se ha realizado correctamente, o cero para indicar un error.|

```
void (*Free)();
```
Nombre del marcador de posición para una función de finalización definida por el proveedor. El controlador puede llamar a esta función tras la terminación normal del proceso.

> [!NOTE]
> *Las cadenas de caracteres anchos son caracteres de 2 bytes (UTF-16) debido a cómo SQL Server las almacena.*


### <a name="error-handling"></a>Tratamiento de errores

A medida que se produzcan errores durante el procesamiento de un proveedor, se proporciona un mecanismo para que pueda notificar los errores de vuelta al controlador en detalles más específicos que un error o éxito booleano. Muchas de las funciones tienen un par de parámetros, **CTX** y **OnError**, que se usan juntos para este propósito, además del valor devuelto de éxito o error.

El parámetro **CTX** identifica el contexto en el que se produce una operación de proveedor.

El parámetro **OnError** apunta a una función de generación de informes de errores, con el prototipo siguiente:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|Argumento|Descripción|
|:--|:--|
|`ctx`|Entradas Contexto en el que se va a notificar el error.|
|`msg`|Entradas Mensaje de error que se va a notificar. Cadena de caracteres anchos terminada en NULL. Para permitir que la información parametrizada esté presente, esta cadena puede contener secuencias de formato de inserción del formato aceptado por la función [FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage) . Este parámetro puede especificar la funcionalidad extendida, tal y como se describe a continuación.|
|…|Entradas Parámetros variádicas adicionales para ajustar los especificadores de formato en MSG, según corresponda.|

Para notificar cuando se ha producido un error, el proveedor llama a OnError, proporcionando el parámetro de contexto pasado a la función de proveedor por el controlador y un mensaje de error con parámetros adicionales opcionales a los que se les va a dar formato. El proveedor puede llamar varias veces a esta función para enviar varios mensajes de error consecutivamente dentro de una invocación de función de proveedor. Por ejemplo:

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


Normalmente `msg` , el parámetro es una cadena de caracteres anchos, pero hay extensiones adicionales disponibles:

Mediante el uso de uno de los valores predefinidos especiales con la macro IDS_MSG, se pueden usar los mensajes de error genéricos ya existentes y en una forma localizada en el controlador. Por ejemplo, si un proveedor no puede asignar memoria, se `IDS_S1_001` puede usar el mensaje "error de asignación de memoria":

`onError(ctx, IDS_MSG(IDS_S1_001));`

Para que el controlador reconozca el error, la función de proveedor debe devolver un error. Cuando esto se realiza en el contexto de una operación ODBC, los errores expuestos se volverán accesibles en el identificador de la conexión o la instrucción a través del`SQLError`mecanismo `SQLGetDiagRec`de diagnóstico `SQLGetDiagField`estándar de ODBC (, y).


### <a name="context-association"></a>Asociación de contexto

La `CEKEYSTORECONTEXT` estructura, además de proporcionar el contexto para la devolución de llamada de error, también se puede usar para determinar el contexto ODBC en el que se ejecuta una operación de proveedor. Esto permite a un proveedor asociar datos a cada uno de estos contextos, por ejemplo, para implementar la configuración por conexión. Para este propósito, la estructura contiene tres punteros opacos correspondientes al entorno, la conexión y el contexto de la instrucción:

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
|`envCtx`|Contexto del entorno.|
|`dbcCtx`|Contexto de la conexión.|
|`stmtCtx`|Contexto de la instrucción.|

Cada uno de estos contextos es un valor opaco que, aunque no es el mismo que el identificador ODBC correspondiente, se puede usar como identificador único para el identificador: Si el identificador *X* está asociado con el valor de contexto *y*, no hay otro entorno, conexión ni los identificadores de instrucciones que existen simultáneamente al mismo tiempo que *X* tendrán un valor de *contexto de y*, y no se asociarán otros valores de contexto al identificador *X*. Si la operación del proveedor que se va a realizar no tiene un contexto de identificador determinado (por ejemplo, las llamadas de SQLSetConnectAttr para cargar y configurar proveedores, en los que no hay ningún identificador de instrucción) el valor de contexto correspondiente en la estructura es NULL.


## <a name="example"></a>Ejemplo

### <a name="keystore-provider"></a>Proveedor de almacén de claves

El código siguiente es un ejemplo de una implementación mínima del proveedor de almacén de claves.

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

### <a name="odbc-application"></a>Aplicación ODBC

El código siguiente es una aplicación de demostración que usa el proveedor de almacén de claves anterior. Al ejecutarlo, asegúrese de que la biblioteca del proveedor está en el mismo directorio que el archivo binario de la aplicación y que la cadena de conexión especifica (o especifica `ColumnEncryption=Enabled` un DSN que contiene) el valor.

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
