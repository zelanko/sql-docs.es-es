---
title: "Los proveedores de almacén de claves personalizado | Documentos de Microsoft"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
caps.latest.revision: 1
ms.author: v-chojas
manager: jhubbard
author: MightyPen
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd6d86df2ec743376af34ac93d8b746bbe0a6eb3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="custom-keystore-providers"></a>Proveedores de almacén de claves personalizados
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Información general

La característica de cifrado de columna de SQL Server 2016 requiere que el cifrado columna claves de cifrado (ECEKs) almacenadas en el servidor de ser recuperadas por el cliente y, a continuación, descifra a claves de cifrado de columna (las CEK) para tener acceso a los datos almacenados en columnas cifradas. ECEKs se cifran con claves maestras de columna (CMK) y la seguridad de la CMK es importante para la seguridad del cifrado de columna. Por lo tanto, la CMK debe almacenarse en una ubicación segura; el propósito de un proveedor de almacén de claves de cifrado de columna es proporcionar una interfaz para permitir que el controlador ODBC tener acceso a ellos de forma segura almacenados CMK. Para los usuarios con su propio almacenamiento seguro, la interfaz del proveedor de almacén de claves personalizado proporciona un marco de trabajo para implementar el acceso para proteger el almacenamiento de la CMK para el controlador ODBC, que, a continuación, se puede usar para realizar CEK cifrado y descifrado.

Cada proveedor de almacén de claves contiene y administra uno o más CMK, que se identifica mediante rutas de acceso de claves: las cadenas de un formato definido por el proveedor. Esto, junto con el algoritmo de cifrado también una cadena definida por el proveedor, puede utilizarse para realizar el cifrado de una CEK y el descifrado de una ECEK. El algoritmo, junto con el ECEK y el nombre del proveedor, se almacenan en los metadatos de cifrado de la base de datos; vea [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) y [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) para obtener más información. Por tanto, las dos operaciones fundamentales de administración de claves son:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

donde la `CEKeystoreProvider_name` se usa para identificar el proveedor de almacén de claves de cifrado específico de columna (CEKeystoreProvider), y el resto de argumentos que se usa por el CEKeystoreProvider para cifrar o descifrar la CEK (E). El nombre y la ruta de acceso clave se proporcionan los metadatos de CMK, mientras que el algoritmo y el valor ECEK se proporcionan los metadatos CEK. Varios proveedores de almacén de claves pueden encontrarse junto con los proveedores integrados de forma predeterminada. Al realizar una operación que requiere la CEK, el controlador utiliza los metadatos CMK para buscar el proveedor de almacén de claves adecuado por el nombre y ejecuta la operación de descifrado, que se puede expresar como:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

Aunque el controlador no tiene ninguna necesidad de cifran las CEK, una herramienta de administración de claves que necesite hacerlo para implementar operaciones como la creación de CMK y rotación; Para ello, realiza la operación inversa:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>Interfaz CEKeyStoreProvider

Este documento describe detalladamente la interfaz CEKeyStoreProvider. Un proveedor de almacén de claves que implementa esta interfaz se puede utilizar el controlador ODBC de Microsoft para SQL Server. Los implementadores de CEKeyStoreProvider pueden utilizar a esta guía para desarrollar proveedores de almacén de claves personalizado puede utilizarlos el controlador.

Una biblioteca de proveedor de almacén de claves ("biblioteca de proveedor") es una biblioteca de vínculos dinámicos que se puede cargar el controlador ODBC y contiene uno o varios proveedores de almacén de claves. El símbolo `CEKeystoreProvider` debe exportarse en una biblioteca de proveedor y la dirección de una matriz terminada en null de punteros a `CEKeystoreProvider` estructuras, uno para cada proveedor de almacén de claves dentro de la biblioteca.

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

|Nombre de campo|Description|
|:--|:--|
|`Name`|El nombre del proveedor de almacén de claves. No debe ser igual que cualquier otro proveedor de almacén de claves previamente cargado por el controlador o está presente en esta biblioteca. Terminada en null, amplia-cadena de caracteres.|
|`Init`|Función de inicialización. Si una función de inicialización no es necesaria, este campo puede ser null.|
|`Read`|Proveedor read (función). Puede ser null si no es necesario.|
|`Write`|Función de escritura de proveedor. Requerido si lectura no es null. Puede ser null si no es necesario.|
|`DecryptCEK`|Función de descifrado de ECEK. Esta función es la razón de la existencia de un proveedor de almacén de claves y no debe ser null.|
|`EncryptCEK`|Función de cifrado CEK. El controlador no llama a esta función, pero se proporciona para permitir el acceso mediante programación a la creación de ECEK con herramientas de administración de claves. Puede ser null si no es necesario.|
|`Free`|Función de finalización. Puede ser null si no es necesario.|

Con la excepción Free, las funciones en esta interfaz todos tienen un par de parámetros, **ctx** y **onError**. El primero identifica el contexto en el que se llama a la función, mientras que se utiliza para notificar errores. Vea [contextos](#context-association) y [control de errores](#error-handling) a continuación para obtener más información.

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
Nombre de marcador de posición para una función de inicialización definidos por el proveedor. El controlador llama a esta función una vez, después de un proveedor se ha cargado, pero antes de la primera vez debe llevar a cabo el descifrado de ECEK o Read()/Write() solicita. Use esta función para realizar cualquier inicialización que necesita. 

|Argumento|Description|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de informe de errores.|
|`Return Value`|Devolver es distinto de cero para indicar el éxito o cero para indicar el error.|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

Nombre de marcador de posición para una función definida por el proveedor de comunicación. El controlador llama a esta función cuando la aplicación solicita para leer datos de un (previamente escrito-a) proveedor utilizando el atributo de conexión SQL_COPT_SS_CEKEYSTOREDATA, permitir que la aplicación leer datos arbitrarios desde el proveedor. Vea [comunicarse con los proveedores de almacén de claves](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) para obtener más información.

|Argumento|Description|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de informe de errores.|
|`data`|[Salida] Puntero a un búfer en el que el proveedor escribe los datos para ser leídos por la aplicación. Esto corresponde al campo de datos de la estructura CEKEYSTOREDATA.|
|`len`|[Entrada] Puntero a un valor de longitud; durante la entrada, se trata de la longitud máxima del búfer de datos y el proveedor no se debe escribir más de * len bytes a él. Tras la devolución, debe actualizar el proveedor * len con el número de bytes escritos realmente.|
|`Return Value`|Devolver es distinto de cero para indicar el éxito o cero para indicar el error.|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
Nombre de marcador de posición para una función definida por el proveedor de comunicación. El controlador llama a esta función cuando la aplicación solicita para escribir datos en un proveedor mediante el atributo de conexión SQL_COPT_SS_CEKEYSTOREDATA, permitir que la aplicación escribir datos arbitrarios en el proveedor. Vea [comunicarse con los proveedores de almacén de claves](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) para obtener más información.

|Argumento|Description|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de informe de errores.|
|`data`|[Entrada] Puntero a un búfer que contiene los datos para el proveedor leer. Esto corresponde al campo de datos de la estructura CEKEYSTOREDATA. El proveedor no debe leer más bytes de longitud de este búfer.|
|`len`|[Entrada] El número de bytes disponibles en los datos. Esto corresponde al campo de la estructura CEKEYSTOREDATA dataSize.|
|`Return Value`|Devolver es distinto de cero para indicar el éxito o cero para indicar el error.|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
Nombre de marcador de posición para una función de descifrado de ECEK definida por el proveedor. El controlador llama a esta función para descifrar un cifrado por una CMK asociada a este proveedor en una CEK de ECEK.

|Argumento|Description|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de informe de errores.|
|`keyPath`|[Entrada] El valor de la [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) atributo de metadatos para la CMK al que hace referencia el ECEK determinado. Terminada en nulo ancho-cadena de caracteres. Esto está pensado para identificar una CMK controlada por este proveedor.|
|`alg`|[Entrada] El valor de la [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) atributo de metadatos para el ECEK determinado. Terminada en nulo ancho-cadena de caracteres. Esto está pensado para identificar el algoritmo de cifrado usado para cifrar el ECEK determinado.|
|`ecek`|[Entrada] Puntero a la ECEK deben descifrarse.|
|`ecekLen`|[Entrada] Longitud de la ECEK.|
|`cekOut`|[Salida] El proveedor debe asignar memoria para el descifrado ECEK y escribir su dirección en el puntero que señala cekOut. Debe ser posible liberar este bloque de memoria utilizando la [LocalFree](https://msdn.microsoft.com/library/windows/desktop/aa366730(v=vs.85).aspx) (Windows) o liberar (función) (Linux/Mac). Si no había memoria asignada debido a un error o en caso contrario, el proveedor debe establecer * cekOut a un puntero null.|
|`cekLen`|[Salida] El proveedor deberá escribir en la dirección que señala cekLen la longitud de la ECEK descifrado que ha escrito en ** cekOut.|
|`Return Value`|Devolver es distinto de cero para indicar el éxito o cero para indicar el error.|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
Nombre de marcador de posición para una función definida por el proveedor de cifrado de CEK. El controlador no llame a esta función ni exponer su funcionalidad a través de la interfaz ODBC, pero se proporciona para permitir el acceso mediante programación a la creación de ECEK con herramientas de administración de claves.

|Argumento|Description|
|:--|:--|
|`ctx`|[Entrada] Contexto de la operación.|
|`onError`|[Entrada] Función de informe de errores.|
|`keyPath`|[Entrada] El valor de la [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) atributo de metadatos para la CMK al que hace referencia el ECEK determinado. Terminada en nulo ancho-cadena de caracteres. Esto está pensado para identificar una CMK controlada por este proveedor.|
|`alg`|[Entrada] El valor de la [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) atributo de metadatos para el ECEK determinado. Terminada en nulo ancho-cadena de caracteres. Esto está pensado para identificar el algoritmo de cifrado usado para cifrar el ECEK determinado.|
|`cek`|[Entrada] Puntero a la CEK se cifren.|
|`cekLen`|[Entrada] Longitud de la CEK.|
|`ecekOut`|[Salida] El proveedor debe asignar memoria para la CEK cifrada y escribir su dirección en el puntero que señala ecekOut. Debe ser posible liberar este bloque de memoria utilizando la [LocalFree](https://msdn.microsoft.com/library/windows/desktop/aa366730(v=vs.85).aspx) (Windows) o liberar (función) (Linux/Mac). Si no había memoria asignada debido a un error o en caso contrario, el proveedor debe establecer * ecekOut a un puntero null.|
|`ecekLen`|[Salida] El proveedor deberá escribir en la dirección que señala ecekLen la longitud de la CEK cifrada que ha escrito en ** ecekOut.|
|`Return Value`|Devolver es distinto de cero para indicar el éxito o cero para indicar el error.|

```
void (*Free)();
```
Nombre de marcador de posición para una función definida por el proveedor de terminación. El controlador puede llamar a esta función tras la finalización normal del proceso.

> [!NOTE]
> *Cadenas de caracteres anchos son caracteres de 2 bytes (UTF-16) debido al modo en que se almacena SQL Server.*


### <a name="error-handling"></a>Tratamiento de errores

Como pueden producirse errores durante el procesamiento de un proveedor de servicios, se proporciona un mecanismo para permitir que se informe de errores al controlador con más detalle que un correcto o con errores booleano. Muchas de las funciones tienen un par de parámetros, **ctx** y **onError**, que se utilizan conjuntamente para este propósito, además del valor devuelto de correcto o con errores.

El **ctx** parámetro identifica el contexto en el que se produce una operación de proveedor.

El **onError** parámetro señala a una función de informe de errores, con el prototipo siguiente:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|Argumento|Description|
|:--|:--|
|`ctx`|[Entrada] El contexto para notificar el error en.|
|`msg`|[Entrada] El mensaje de error al informe. Cadena terminada en null de caracteres anchos. Para permitir que se presente la información con parámetros, esta cadena puede contener secuencias de formato para insertar el formato aceptado por la [FormatMessage](https://msdn.microsoft.com/library/windows/desktop/ms679351(v=vs.85).aspx) función. Funcionalidad extendida se puede especificar mediante este parámetro, tal y como se describe a continuación.|
|...|[Entrada] Parámetros de variádicas adicionales para ajustar los especificadores de formato de mensaje, según corresponda.|

Para notificar cuando se ha producido un error, el onError de llamadas de proveedor, proporcione el parámetro de contexto pasados a la función de proveedor por el controlador y un mensaje de error con los parámetros opcionales adicionales se formateen en él. El proveedor puede llamar a esta función varias veces para enviar varios mensajes de error consecutivamente dentro de la invocación de una función de proveedor. Por ejemplo:

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


El `msg` parámetro normalmente es una cadena de caracteres anchos, pero las extensiones adicionales están disponibles:

Pueden utilizarse mediante uno de los valores predefinidos especiales con la macro IDS_MSG, mensajes de error genéricos existentes y en un formulario localizado en el controlador. Por ejemplo, si un proveedor no puede asignar memoria, el `IDS_S1_001` mensaje "Error de asignación de memoria" se puede usar:

`onError(ctx, IDS_MSG(IDS_S1_001));`

Para que el error para ser reconocidos por el controlador, la función de proveedor debe devolver el error. Cuando esto se realiza en el contexto de una operación de ODBC, los errores registrados estará accesibles en el identificador de conexión o instrucción a través del mecanismo de diagnóstico estándar de ODBC (`SQLError`, `SQLGetDiagRec`, y `SQLGetDiagField`).


### <a name="context-association"></a>Asociación de contexto

El `CEKEYSTORECONTEXT` estructura, además de proporcionar el contexto de la devolución de llamada de error, también puede utilizarse para determinar el contexto ODBC en el que se ejecuta una operación de proveedor. Esto permite que un proveedor asociar los datos a cada uno de estos contextos, por ejemplo, para implementar la configuración de cada conexión. Para ello, la estructura contiene 3 punteros opacos correspondiente en el contexto del entorno, conexión e instrucción:

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```
|Campo|Description|
|:--|:--|
|`envCtx`|Contexto del entorno.|
|`dbcCtx`|Contexto de conexión.|
|`stmtCtx`|Contexto de la instrucción.|

Cada uno de estos contextos es un valor opaco que, al no es igual que el controlador ODBC correspondiente, se puede usar como un identificador único para el identificador: si controlar *X* está asociado con el valor de contexto *Y*, a continuación, No hay otros identificadores entorno, conexión o instrucción que existen simultáneamente al mismo tiempo como *X* tendrá un valor de contexto de *Y*, y no se asociará ningún otro valor de contexto controlar *X*. Si está llevando a cabo la operación de proveedor no tiene un contexto de controlador determinado (por ejemplo, llamadas de SQLSetConnectAttr para cargar y configurar los proveedores, en el que no hay ningún identificador de instrucción) correspondiente valor de contexto de la estructura es null.


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

El código siguiente es una aplicación de demostración que usa el proveedor de almacén de claves anterior. Cuando se ejecuta, asegúrese de que la biblioteca del proveedor está en el mismo directorio que el archivo binario de la aplicación, y que especifica la cadena de conexión (o especifica un DSN que contiene) la `ColumnEncryption=Enabled` configuración.

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

## <a name="see-also"></a>Vea también

[Uso de Always Encrypted con el controlador ODBC](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)

