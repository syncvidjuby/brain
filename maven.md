
Maven
---

### Scopes

<table>
	<tr>
		<td>Scope</td>
		<td>Description</td>
		<td>Transitive</td>
		<td>Example</td>
	</tr>
	<tr>
		<td>Compile</td>
		<td>Default scope</td>
		<td>runtime scope will be pulled in with the runtime scope, compile scope will be pulled in with the compile scope</td>
		<td></td>
	</tr>
	<tr>
		<td>Provided</td>
		<td>Dependencies that should be provided at runtime by JDK or a container</td>
		<td>runtime and compile scope dependencies will be pulled in with the provided scope</td>
		<td>jakarta.servlet-api</td>
	</tr>
	<tr>
		<td>Runtime</td>
		<td>The dependencies with this scope are required at runtime</td>
		<td>runtime and compile scope transitive dependencies will be pulled in with the runtime scope</td>
		<td>JDBC driver</td>
	</tr>
	<tr>
		<td>Test</td>
		<td>Present only for test</td>
		<td>runtime and compile scope transitive dependencies will be pulled in with the test scope</td>
		<td></td>
	</tr>
	<tr>
		<td>System</td>
		<td>Same as Provided but directly point to local jar on system</td>
		<td></td>
		<td></td>
	</tr>
	<tr>
		<td>Import</td>
		<td>Import indicates that this dependency should be replaced with all effective dependencies declared in its POM </td>
		<td></td>
		<td></td>
	</tr>
</table>
