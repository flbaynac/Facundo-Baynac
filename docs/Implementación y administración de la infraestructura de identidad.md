---
share: "true"
---
# [Introducción a AD DS](https://learn.microsoft.com/es-es/training/modules/introduction-to-ad-ds/)
## Componentes lógicos y físicos 
### Lógicos:
#### Partición
Una partición, o contexto de nomenclatura, es una parte de la base de datos de AD DS. Aunque la base de datos consta de un archivo denominado Ntds.dit, las diferentes particiones contienen datos diferentes. Por ejemplo, la partición de esquema contiene una copia del esquema de Active Directory
#### Schema
Un esquema es el conjunto de definiciones de los tipos de objeto y los atributos que se usan para definir los objetos creados en AD DS
#### Domain
Un dominio es un contenedor administrativo lógico para objetos como usuarios y equipos
#### Árbol de dominios
Un árbol de dominios es una colección jerárquica de dominios que comparten un dominio raíz común y un espacio de nombres del sistema de nombres de dominio (DNS) contiguo.
#### Bosque
Un bosque es una colección de uno o varios dominios que tienen una raíz AD DS común, un esquema común y un catálogo global común
#### Unidad Organizativa
Una unidad organizativa es un objeto contenedor de usuarios, grupos y equipos que proporciona un marco para la delegación de derechos administrativos y la administración mediante la vinculación de objetos de directiva de grupo (GPO)
#### Contenedor
Un contenedor es un objeto que proporciona un marco de organización para su uso en AD DS. Puede usar los contenedores predeterminados o bien crear contenedores personalizados. No se pueden vincular GPO a contenedores
### Físicos
#### Controlador de dominio
Un controlador de dominio contiene una copia de la base de datos de AD DS. Para la mayoría de las operaciones, cada controlador de dominio puede procesar los cambios y replicarlos en todos los demás controladores de dominio del dominio
#### Almacén de datos
Existe una copia del almacén de datos en cada controlador de dominio. La base de datos de AD DS usa la tecnología de base de datos Microsoft Jet y almacena la información de directorio en el archivo Ntds.dit y en los archivos de registro asociados. La carpeta `C:\Windows\NTDS` almacena estos archivos de forma predeterminada
#### Servidor del catálogo global
Un servidor del catálogo global es un controlador de dominio que hospeda el catálogo global, que es una copia parcial de solo lectura de todos los objetos de un bosque de varios dominios. Un catálogo global acelera las búsquedas de objetos que pueden estar almacenados en controladores de un dominio diferente del bosque
#### Controlador de dominio de solo lectura (`RODC`)
Un RODC es una instalación especial de solo lectura de AD DS. Los RODC son comunes en las sucursales donde la seguridad física no es óptima, el soporte de TI es menos avanzado que en los centros corporativos principales, o las aplicaciones de línea de negocio necesitan ejecutarse en un controlador de dominio
#### Sitio
Un sitio es un contenedor de objetos de AD DS, como equipos y servicios que son específicos de una ubicación física. Esto es en comparación con un dominio, que representa la estructura lógica de objetos, como usuarios y grupos, además de los equipos
#### Subnet
Una subred es una parte de las direcciones IP de la red de una organización asignada a los equipos de un sitio. Un sitio puede tener más de una subred

## Usuarios, Grupos y Equipos
### Usuarios:
#### Usuario de dominio: Principalmente contiene: 
- El nombre de usuario.
- Una contraseña de usuario.
- Pertenencias a grupos.
- También contiene parámetros que se pueden configurar en función de los requisitos de la organización. (Puesto, teléfono, etc.)
#### Cuentas de servicio administradas
Se utiliza principalmente para autentificar servicios (programas que se ejecutan en windows server) y que utilicen funcionalidades del dominio. Es símil a una cuenta local del equipo.
Windows Server admite un objeto de AD DS, denominado cuenta de servicio administrada, que se utiliza para facilitar la administración de la cuenta de servicio. Una cuenta de servicio administrada es una clase de objeto AD DS que permite:
	- Administración simplificada de contraseñas.
	- Administración simplificada de SPN ([Service Principal Name](Service%20Principal%20Name.md)).
#### Cuentas de servicio administradas de grupo (gMSA)
#### Cuentas de servicio administradas delegadas

### Grupos:
#### Tipos:
* Seguridad
* Distribución
#### Ámbito:
* Local
* Local de dominio
* Global
* Universal
### Equipos:
 
# [Administración de controladores de dominio de AD DS y roles de FSMO](https://learn.microsoft.com/es-es/training/modules/manage-active-directory-domain-services-flexible-single-master-operation-roles/)

# [Implementación de objetos de directiva de grupo](https://learn.microsoft.com/es-es/training/modules/implement-group-policy-objects/)

# [Administración de características avanzadas de AD DS](https://learn.microsoft.com/es-es/training/modules/manage-advanced-features-of-ad-ds/)

# [Implementación de la nube híbrida con Windows Server](https://learn.microsoft.com/es-es/training/modules/implement-hybrid-identity-windows-server/)

# [Implementación y administración de controladores de dominio de Active Directory de IaaS de Azure en Azure](https://learn.microsoft.com/es-es/training/modules/deploy-manage-azure-iaas-active-directory-domain-controllers-azure/)
