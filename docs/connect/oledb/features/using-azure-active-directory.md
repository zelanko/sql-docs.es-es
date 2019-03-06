---
title: Uso de Azure Active Directory | Documentos de Microsoft para SQL Server
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 44f92e782a497005ea47847301279e4341722d36
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744860"
---
# <a name="using-azure-active-directory"></a>Uso de Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>Finalidad

Controlador OLE DB de Microsoft para SQL Server a partir de versión 18.2.1, permite a las aplicaciones OLE DB para conectarse a una instancia de Azure SQL Database con una identidad federada. Los nuevos métodos de autenticación se incluyen:
- Identificador de inicio de sesión de Azure Active Directory y la contraseña
- Token de acceso de Azure Active Directory
- Autenticación integrada de Azure Active Directory
- Id. de inicio de sesión SQL y la contraseña

> [!NOTE]  
> Al usar las siguientes opciones de Azure Active Directory con el controlador OLE DB, asegúrese de que el [Active Directory Authentication Library para SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) se ha instalado:
> - Identificador de inicio de sesión de Azure Active Directory y la contraseña
> - Autenticación integrada de Azure Active Directory
>
> ADAL no es necesario para los otros métodos de autenticación o las operaciones de OLE DB.

> [!NOTE]
> Uso de los siguientes modos de autenticación con `DataTypeCompatibility` (o la propiedad correspondiente) establecido en `80` es **no** admite:
> - Autenticación de Azure Active Directory con Id. de inicio de sesión y la contraseña
> - Autenticación de Azure Active Directory mediante el token de acceso
> - Autenticación integrada de Azure Active Directory

## <a name="connection-string-keywords-and-properties"></a>Las propiedades y palabras clave de cadena de conexión
Se han introducido las siguientes palabras clave de cadena de conexión para admitir la autenticación de Azure Active Directory:

|Palabra clave de cadena de conexión|Propiedad Conexión|Descripción|
|---               |---                |---        |
|Token de acceso|SSPROP_AUTH_ACCESS_TOKEN|Especifica un token de acceso para autenticarse en Azure Active Directory. |
|Autenticación|SSPROP_AUTH_MODE|Especifica el método de autenticación utilizar.|

Para obtener más información acerca de las nuevas palabras clave y propiedades, vea las páginas siguientes:
- [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [Propiedades de inicialización y autorización](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>Cifrado y validación de certificados
En esta sección se describe los cambios en el cifrado y el comportamiento de validación de certificados. Estos cambios son **sólo** en vigor cuando se usa la nueva autenticación o el Token de acceso de conexión palabras clave de cadena (o sus propiedades correspondientes).

### <a name="encryption"></a>Cifrado
Para mejorar la seguridad, cuando se usan las nuevas propiedades/palabras clave de conexión, el controlador invalida el valor de cifrado predeterminado si se establece en `yes`. Reemplazar se produce en tiempo de inicialización de objeto de origen de datos. Si el cifrado se establece antes de la inicialización por ningún medio, el valor se respeta y no se reemplaza.

> [!NOTE]   
> En las aplicaciones ADO y en aplicaciones que obtienen el `IDBInitialize` a través de la interfaz `IDataInitialize::GetDataSource`, Establece que el componente principal que implementa la interfaz explícitamente cifrado en su valor predeterminado de `no`. Como resultado, la nueva autenticación propiedades o palabras clave respeta esta configuración y el valor cifrado **no** se reemplaza. Por lo tanto, resulta **recomienda** que establezca explícitamente estas aplicaciones `Use Encryption for Data=true` para invalidar el valor predeterminado.

### <a name="certificate-validation"></a>Validación de certificados
Para mejorar la seguridad, la nueva conexión propiedades o palabras clave respetan la `TrustServerCertificate` configuración (y sus correspondientes palabras clave cadena de conexión/propiedades) **independientemente de la configuración de cifrado de cliente**. Como resultado, se valida el certificado de servidor de forma predeterminada.

> [!NOTE]   
> También se puede controlar la validación de certificados a través de la `Value` campo de la `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2` entrada del registro. Los valores válidos son `0` y `1`. El controlador OLE DB elige la opción más segura entre el registro y la configuración de la propiedad y palabras clave de conexión. Es decir, el controlador validará el certificado de servidor, siempre y cuando al menos uno de los valores del registro y conexión habilita la validación de certificado de servidor.

## <a name="gui-additions"></a>Adiciones de interfaz gráfica de usuario
La interfaz gráfica de usuario del controlador se ha mejorado para permitir la autenticación de Azure Active Directory. Para obtener más información, vea:
- [Cuadro de diálogo de inicio de sesión de SQL Server](../help-topics/sql-server-login-dialog.md)
- [Configuración de Universal Data Link (UDL)](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>Ejemplos de cadena de conexión
En esta sección se muestra ejemplos de conexión nuevo y existente para usarse con palabras clave de cadena `IDataInitialize::GetDataSource` y `DBPROP_INIT_PROVIDERSTRING` propiedad.

### <a name="sql-authentication"></a>Autenticación SQL
- Usar `IDataInitialize::GetDataSource`:
    - Nuevo:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=SqlPassword**;User ID=[username];Password=[password];Use Encryption for Data=true
    - Obsoleto:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];User ID=[username];Password=[password];Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    - Nuevo:
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - Obsoleto:
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface--sspi"></a>Autenticación integrada de Windows mediante la interfaz de proveedor de compatibilidad para seguridad (SSPI)

- Usar `IDataInitialize::GetDataSource`:
    - Nuevo:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
    - Obsoleto:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Integrated Security=SSPI**;Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    - Nuevo:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - Obsoleto:
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="aad-username-and-password-authentication-using-adal"></a>Nombre de usuario y contraseña de la autenticación de AAD mediante ADAL

- Usar `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryPassword**;User ID=[username];Password=[password];Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-azure-active-directory-authentication-using-adal"></a>Autenticación integrada de Azure Active Directory mediante ADAL

- Usar `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>Autenticación de Azure Active Directory con un token de acceso

- Usar `IDataInitialize::GetDataSource`:
    > Proveedor = MSOLEDBSQL; origen de datos = [server]; Initial Catalog = [database]; **Token de acceso = [token de acceso]**; Usar el cifrado de datos = true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    > Token de acceso que proporciona a través de `DBPROP_INIT_PROVIDERSTRING` no se admite

## <a name="code-samples"></a>Ejemplos de código

Los ejemplos siguientes muestran el código necesario para conectarse a Azure Active Directory con palabras clave de conexión. 

### <a name="access-token"></a>Token de acceso
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    wchar_t accessToken[] = L"eyJ0eXAiOi...";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Access Token=" + accessToken + L";Use Encryption for Data=true;";
    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```
### <a name="active-directory-integrated"></a>Active Directory Integrated
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr)) 
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```

## <a name="next-steps"></a>Pasos siguientes
- [Autorizar el acceso a las aplicaciones web de Azure Active Directory mediante el flujo de concesión de código de OAuth 2.0](https://go.microsoft.com/fwlink/?linkid=2072672).

- Aprenda más sobre la [autenticación de Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=2073783) a SQL Server.

- Configuración de conexiones de controlador mediante [palabras clave de cadena de conexión](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) el controlador OLE DB admite.
