---
title: API Reference
---
# HyperShift API Reference
<p>Packages:</p>
<ul>
<li>
<a href="#hypershift.openshift.io%2fv1alpha1">hypershift.openshift.io/v1alpha1</a>
</li>
</ul>
<h2 id="hypershift.openshift.io/v1alpha1">hypershift.openshift.io/v1alpha1</h2>
<p>
<p>Package v1alpha1 contains the HyperShift API.</p>
<p>The HyperShift API enables creating and managing lightweight, flexible, heterogeneous
OpenShift clusters at scale.</p>
<p>HyperShift clusters are deployed in a topology which isolates the &ldquo;control plane&rdquo;
(e.g. etcd, the API server, controller manager, etc.) from the &ldquo;data plane&rdquo; (e.g.
worker nodes and their kubelets, and the infrastructure on which they run). This
enables &ldquo;hosted control plane as a service&rdquo; use cases.</p>
</p>
##HostedCluster { #hypershift.openshift.io/v1alpha1.HostedCluster }
<p>
<p>HostedCluster is the primary representation of a HyperShift cluster and encapsulates
the control plane and common data plane configuration. Creating a HostedCluster
results in a fully functional OpenShift control plane with no attached nodes.
To support workloads (e.g. pods), a HostedCluster may have one or more associated
NodePool resources.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>apiVersion</code></br>
string</td>
<td>
<code>
hypershift.openshift.io/v1alpha1
</code>
</td>
</tr>
<tr>
<td>
<code>kind</code></br>
string
</td>
<td><code>HostedCluster</code></td>
</tr>
<tr>
<td>
<code>metadata</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#objectmeta-v1-meta">
Kubernetes meta/v1.ObjectMeta
</a>
</em>
</td>
<td>
Refer to the Kubernetes API documentation for the fields of the
<code>metadata</code> field.
</td>
</tr>
<tr>
<td>
<code>spec</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">
HostedClusterSpec
</a>
</em>
</td>
<td>
<p>Spec is the desired behavior of the HostedCluster.</p>
<br/>
<br/>
<table>
<tr>
<td>
<code>release</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.Release">
Release
</a>
</em>
</td>
<td>
<p>Release specifies the desired OCP release payload for the hosted cluster.</p>
<p>Updating this field will trigger a rollout of the control plane. The
behavior of the rollout will be driven by the ControllerAvailabilityPolicy
and InfrastructureAvailabilityPolicy.</p>
</td>
</tr>
<tr>
<td>
<code>infraID</code></br>
<em>
string
</em>
</td>
<td>
<p>InfraID is a globally unique identifier for the cluster. This identifier
will be used to associate various cloud resources with the HostedCluster
and its associated NodePools.</p>
<p>TODO(dan): consider moving this to .platform.aws.infraID</p>
</td>
</tr>
<tr>
<td>
<code>platform</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.PlatformSpec">
PlatformSpec
</a>
</em>
</td>
<td>
<p>Platform specifies the underlying infrastructure provider for the cluster
and is used to configure platform specific behavior.</p>
</td>
</tr>
<tr>
<td>
<code>controllerAvailabilityPolicy</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AvailabilityPolicy">
AvailabilityPolicy
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ControllerAvailabilityPolicy specifies the availability policy applied to
critical control plane components. The default value is SingleReplica.</p>
<p>
Value must be one of:
&#34;HighlyAvailable&#34;, 
&#34;SingleReplica&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>infrastructureAvailabilityPolicy</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AvailabilityPolicy">
AvailabilityPolicy
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>InfrastructureAvailabilityPolicy specifies the availability policy applied
to infrastructure services which run on cluster nodes. The default value is
HighlyAvailable.</p>
<p>
Value must be one of:
&#34;HighlyAvailable&#34;, 
&#34;SingleReplica&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>dns</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.DNSSpec">
DNSSpec
</a>
</em>
</td>
<td>
<p>DNS specifies DNS configuration for the cluster.</p>
</td>
</tr>
<tr>
<td>
<code>networking</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterNetworking">
ClusterNetworking
</a>
</em>
</td>
<td>
<p>Networking specifies network configuration for the cluster.</p>
</td>
</tr>
<tr>
<td>
<code>autoscaling</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterAutoscaling">
ClusterAutoscaling
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Autoscaling specifies auto-scaling behavior that applies to all NodePools
associated with the control plane.</p>
</td>
</tr>
<tr>
<td>
<code>etcd</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.EtcdSpec">
EtcdSpec
</a>
</em>
</td>
<td>
<p>Etcd specifies configuration for the control plane etcd cluster. The
default ManagementType is Managed. Once set, the ManagementType cannot be
changed.</p>
</td>
</tr>
<tr>
<td>
<code>services</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ServicePublishingStrategyMapping">
[]ServicePublishingStrategyMapping
</a>
</em>
</td>
<td>
<p>Services specifies how individual control plane services are published from
the hosting cluster of the control plane.</p>
<p>If a given service is not present in this list, it will be exposed publicly
by default.</p>
</td>
</tr>
<tr>
<td>
<code>pullSecret</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>PullSecret references a pull secret to be injected into the container
runtime of all cluster nodes. The secret must have a key named
&ldquo;.dockerconfigjson&rdquo; whose value is the pull secret JSON.</p>
</td>
</tr>
<tr>
<td>
<code>sshKey</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>SSHKey references an SSH key to be injected into all cluster node sshd
servers. The secret must have a single key &ldquo;id_rsa.pub&rdquo; whose value is the
public part of an SSH key.</p>
</td>
</tr>
<tr>
<td>
<code>issuerURL</code></br>
<em>
string
</em>
</td>
<td>
<p>IssuerURL is an OIDC issuer URL which is used as the issuer in all
ServiceAccount tokens generated by the control plane API server. The
default value is kubernetes.default.svc, which only works for in-cluster
validation.</p>
</td>
</tr>
<tr>
<td>
<code>configuration</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterConfiguration">
ClusterConfiguration
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Configuration specifies configuration for individual OCP components in the
cluster, represented as embedded resources that correspond to the openshift
configuration API.</p>
</td>
</tr>
<tr>
<td>
<code>auditWebhook</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>AuditWebhook contains metadata for configuring an audit webhook endpoint
for a cluster to process cluster audit events. It references a secret that
contains the webhook information for the audit webhook endpoint. It is a
secret because if the endpoint has mTLS the kubeconfig will contain client
keys. The kubeconfig needs to be stored in the secret with a secret key
name that corresponds to the constant AuditWebhookKubeconfigKey.</p>
<p>This field is currently only supported on the IBMCloud platform.</p>
</td>
</tr>
<tr>
<td>
<code>imageContentSources</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ImageContentSource">
[]ImageContentSource
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ImageContentSources specifies image mirrors that can be used by cluster
nodes to pull content.</p>
</td>
</tr>
<tr>
<td>
<code>secretEncryption</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.SecretEncryptionSpec">
SecretEncryptionSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>SecretEncryption specifies a Kubernetes secret encryption strategy for the
control plane.</p>
</td>
</tr>
<tr>
<td>
<code>fips</code></br>
<em>
bool
</em>
</td>
<td>
<em>(Optional)</em>
<p>FIPS indicates whether this cluster&rsquo;s nodes will be running in FIPS mode.
If set to true, the control plane&rsquo;s ignition server will be configured to
expect that nodes joining the cluster will be FIPS-enabled.</p>
</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>
<code>status</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterStatus">
HostedClusterStatus
</a>
</em>
</td>
<td>
<p>Status is the latest observed status of the HostedCluster.</p>
</td>
</tr>
</tbody>
</table>
##NodePool { #hypershift.openshift.io/v1alpha1.NodePool }
<p>
<p>NodePool is a scalable set of worker nodes attached to a HostedCluster.
NodePool machine architectures are uniform within a given pool, and are
independent of the control plane’s underlying machine architecture.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>apiVersion</code></br>
string</td>
<td>
<code>
hypershift.openshift.io/v1alpha1
</code>
</td>
</tr>
<tr>
<td>
<code>kind</code></br>
string
</td>
<td><code>NodePool</code></td>
</tr>
<tr>
<td>
<code>metadata</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#objectmeta-v1-meta">
Kubernetes meta/v1.ObjectMeta
</a>
</em>
</td>
<td>
Refer to the Kubernetes API documentation for the fields of the
<code>metadata</code> field.
</td>
</tr>
<tr>
<td>
<code>spec</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolSpec">
NodePoolSpec
</a>
</em>
</td>
<td>
<p>Spec is the desired behavior of the NodePool.</p>
<br/>
<br/>
<table>
<tr>
<td>
<code>clusterName</code></br>
<em>
string
</em>
</td>
<td>
<p>ClusterName is the name of the HostedCluster this NodePool belongs to.</p>
<p>TODO(dan): Should this be a LocalObjectReference?</p>
</td>
</tr>
<tr>
<td>
<code>release</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.Release">
Release
</a>
</em>
</td>
<td>
<p>Release specifies the OCP release used for the NodePool. This informs the
ignition configuration for machines, as well as other platform specific
machine properties (e.g. an AMI on the AWS platform).</p>
</td>
</tr>
<tr>
<td>
<code>platform</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolPlatform">
NodePoolPlatform
</a>
</em>
</td>
<td>
<p>Platform specifies the underlying infrastructure provider for the NodePool
and is used to configure platform specific behavior.</p>
</td>
</tr>
<tr>
<td>
<code>nodeCount</code></br>
<em>
int32
</em>
</td>
<td>
<em>(Optional)</em>
<p>NodeCount is the desired number of nodes the pool should maintain. If
unset, the default value is 0.</p>
</td>
</tr>
<tr>
<td>
<code>management</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolManagement">
NodePoolManagement
</a>
</em>
</td>
<td>
<p>Management specifies behavior for managing nodes in the pool, such as
upgrade strategies and auto-repair behaviors.</p>
</td>
</tr>
<tr>
<td>
<code>autoScaling</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolAutoScaling">
NodePoolAutoScaling
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Autoscaling specifies auto-scaling behavior for the NodePool.</p>
</td>
</tr>
<tr>
<td>
<code>config</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
[]Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>Config is a list of references to ConfigMaps containing serialized
MachineConfig resources to be injected into the ignition configurations of
nodes in the NodePool. The MachineConfig API schema is defined here:</p>
<p><a href="https://github.com/openshift/machine-config-operator/blob/master/pkg/apis/machineconfiguration.openshift.io/v1/types.go#L172">https://github.com/openshift/machine-config-operator/blob/master/pkg/apis/machineconfiguration.openshift.io/v1/types.go#L172</a></p>
<p>Each ConfigMap must have a single key named &ldquo;config&rdquo; whose value is the
JSON or YAML of a serialized MachineConfig.</p>
<p>TODO (alberto): this ConfigMaps are meant to contain MachineConfig,
KubeletConfig and ContainerRuntimeConfig but MCO only supports
MachineConfig in bootstrap mode atm. See:
<a href="https://github.com/openshift/machine-config-operator/blob/9c6c2bfd7ed498bfbc296d530d1839bd6a177b0b/pkg/controller/bootstrap/bootstrap.go#L104-L119">https://github.com/openshift/machine-config-operator/blob/9c6c2bfd7ed498bfbc296d530d1839bd6a177b0b/pkg/controller/bootstrap/bootstrap.go#L104-L119</a></p>
</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>
<code>status</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolStatus">
NodePoolStatus
</a>
</em>
</td>
<td>
<p>Status is the latest observed status of the NodePool.</p>
</td>
</tr>
</tbody>
</table>
###AESCBCSpec { #hypershift.openshift.io/v1alpha1.AESCBCSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.SecretEncryptionSpec">SecretEncryptionSpec</a>)
</p>
<p>
<p>AESCBCSpec defines metadata about the AESCBC secret encryption strategy</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>activeKey</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>ActiveKey defines the active key used to encrypt new secrets</p>
</td>
</tr>
<tr>
<td>
<code>backupKey</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>BackupKey defines the old key during the rotation process so previously created
secrets can continue to be decrypted until they are all re-encrypted with the active key.</p>
</td>
</tr>
</tbody>
</table>
###APIServerNetworking { #hypershift.openshift.io/v1alpha1.APIServerNetworking }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterNetworking">ClusterNetworking</a>)
</p>
<p>
<p>APIServerNetworking specifies how the APIServer is exposed inside a cluster
node.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>advertiseAddress</code></br>
<em>
string
</em>
</td>
<td>
<p>AdvertiseAddress is the address that nodes will use to talk to the API
server. This is an address associated with the loopback adapter of each
node. If not specified, 172.20.0.1 is used.</p>
</td>
</tr>
<tr>
<td>
<code>port</code></br>
<em>
int32
</em>
</td>
<td>
<p>Port is the port at which the APIServer is exposed inside a node. Other
pods using host networking cannot listen on this port. If not specified,
6443 is used.</p>
</td>
</tr>
</tbody>
</table>
###AWSCloudProviderConfig { #hypershift.openshift.io/v1alpha1.AWSCloudProviderConfig }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSPlatformSpec">AWSPlatformSpec</a>)
</p>
<p>
<p>AWSCloudProviderConfig specifies AWS networking configuration.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>subnet</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSResourceReference">
AWSResourceReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Subnet is the subnet to use for control plane cloud resources.</p>
</td>
</tr>
<tr>
<td>
<code>zone</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>Zone is the availability zone where control plane cloud resources are
created.</p>
</td>
</tr>
<tr>
<td>
<code>vpc</code></br>
<em>
string
</em>
</td>
<td>
<p>VPC is the VPC to use for control plane cloud resources.</p>
</td>
</tr>
</tbody>
</table>
###AWSEndpointAccessType { #hypershift.openshift.io/v1alpha1.AWSEndpointAccessType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSPlatformSpec">AWSPlatformSpec</a>)
</p>
<p>
<p>AWSEndpointAccessType specifies the publishing scope of cluster endpoints.</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;Private&#34;</p></td>
<td><p>Private endpoint access allows only private API server access and private
node communication with the control plane.</p>
</td>
</tr><tr><td><p>&#34;Public&#34;</p></td>
<td><p>Public endpoint access allows public API server access and public node
communication with the control plane.</p>
</td>
</tr><tr><td><p>&#34;PublicAndPrivate&#34;</p></td>
<td><p>PublicAndPrivate endpoint access allows public API server access and
private node communication with the control plane.</p>
</td>
</tr></tbody>
</table>
###AWSKMSAuthSpec { #hypershift.openshift.io/v1alpha1.AWSKMSAuthSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSKMSSpec">AWSKMSSpec</a>)
</p>
<p>
<p>AWSKMSAuthSpec defines metadata about the management of credentials used to interact with AWS KMS</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>credentials</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>Credentials contains the name of the secret that holds the aws credentials that can be used
to make the necessary KMS calls. It should at key AWSCredentialsFileSecretKey contain the
aws credentials file that can be used to configure AWS SDKs</p>
</td>
</tr>
</tbody>
</table>
###AWSKMSKeyEntry { #hypershift.openshift.io/v1alpha1.AWSKMSKeyEntry }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSKMSSpec">AWSKMSSpec</a>)
</p>
<p>
<p>AWSKMSKeyEntry defines metadata to locate the encryption key in AWS</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>arn</code></br>
<em>
string
</em>
</td>
<td>
<p>ARN is the Amazon Resource Name for the encryption key</p>
</td>
</tr>
</tbody>
</table>
###AWSKMSSpec { #hypershift.openshift.io/v1alpha1.AWSKMSSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.KMSSpec">KMSSpec</a>)
</p>
<p>
<p>AWSKMSSpec defines metadata about the configuration of the AWS KMS Secret Encryption provider</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>region</code></br>
<em>
string
</em>
</td>
<td>
<p>Region contains the AWS region</p>
</td>
</tr>
<tr>
<td>
<code>activeKey</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSKMSKeyEntry">
AWSKMSKeyEntry
</a>
</em>
</td>
<td>
<p>ActiveKey defines the active key used to encrypt new secrets</p>
</td>
</tr>
<tr>
<td>
<code>backupKey</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSKMSKeyEntry">
AWSKMSKeyEntry
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>BackupKey defines the old key during the rotation process so previously created
secrets can continue to be decrypted until they are all re-encrypted with the active key.</p>
</td>
</tr>
<tr>
<td>
<code>auth</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSKMSAuthSpec">
AWSKMSAuthSpec
</a>
</em>
</td>
<td>
<p>Auth defines metadata about the management of credentials used to interact with AWS KMS</p>
</td>
</tr>
</tbody>
</table>
###AWSNodePoolPlatform { #hypershift.openshift.io/v1alpha1.AWSNodePoolPlatform }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolPlatform">NodePoolPlatform</a>)
</p>
<p>
<p>AWSNodePoolPlatform specifies the configuration of a NodePool when operating
on AWS.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>instanceType</code></br>
<em>
string
</em>
</td>
<td>
<p>InstanceType is an ec2 instance type for node instances (e.g. m4-large).</p>
</td>
</tr>
<tr>
<td>
<code>instanceProfile</code></br>
<em>
string
</em>
</td>
<td>
<p>InstanceProfile is TODO</p>
</td>
</tr>
<tr>
<td>
<code>subnet</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSResourceReference">
AWSResourceReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Subnet is the subnet to use for node instances.</p>
</td>
</tr>
<tr>
<td>
<code>ami</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>AMI is the image id to use for node instances. If unspecified, the default
is chosen based on the NodePool release payload image.</p>
</td>
</tr>
<tr>
<td>
<code>securityGroups</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSResourceReference">
[]AWSResourceReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>SecurityGroups is an optional set of security groups to associate with node
instances.</p>
</td>
</tr>
<tr>
<td>
<code>rootVolume</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.Volume">
Volume
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>RootVolume specifies configuration for the root volume of node instances.</p>
</td>
</tr>
<tr>
<td>
<code>resourceTags</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSResourceTag">
[]AWSResourceTag
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ResourceTags is an optional list of additional tags to apply to AWS node
instances.</p>
<p>These will be merged with HostedCluster scoped tags, and HostedCluster tags
take precedence in case of conflicts.</p>
<p>See <a href="https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html">https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html</a> for
information on tagging AWS resources. AWS supports a maximum of 50 tags per
resource. OpenShift reserves 25 tags for its use, leaving 25 tags available
for the user.</p>
</td>
</tr>
</tbody>
</table>
###AWSPlatformSpec { #hypershift.openshift.io/v1alpha1.AWSPlatformSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.PlatformSpec">PlatformSpec</a>)
</p>
<p>
<p>AWSPlatformSpec specifies configuration for clusters running on Amazon Web Services.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>region</code></br>
<em>
string
</em>
</td>
<td>
<p>Region is the AWS region in which the cluster resides. This configures the
OCP control plane cloud integrations, and is used by NodePool to resolve
the correct boot AMI for a given release.</p>
</td>
</tr>
<tr>
<td>
<code>cloudProviderConfig</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSCloudProviderConfig">
AWSCloudProviderConfig
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>CloudProviderConfig specifies AWS networking configuration for the control
plane.</p>
<p>TODO(dan): should this be named AWSNetworkConfig?</p>
</td>
</tr>
<tr>
<td>
<code>serviceEndpoints</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSServiceEndpoint">
[]AWSServiceEndpoint
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ServiceEndpoints specifies optional custom endpoints which will override
the default service endpoint of specific AWS Services.</p>
<p>There must be only one ServiceEndpoint for a given service name.</p>
</td>
</tr>
<tr>
<td>
<code>roles</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSRoleCredentials">
[]AWSRoleCredentials
</a>
</em>
</td>
<td>
<p>Roles must contain exactly 3 entries representing the locators for roles
supporting the following OCP services:</p>
<ul>
<li>openshift-ingress-operator/cloud-credentials</li>
<li>openshift-image-registry/installer-cloud-credentials
-openshift-cluster-csi-drivers/ebs-cloud-credentials</li>
</ul>
<p>Each role has unique permission requirements whose documentation is TBD.</p>
<p>TODO(dan): revisit this field; it&rsquo;s really 3 required fields with specific content requirements</p>
</td>
</tr>
<tr>
<td>
<code>kubeCloudControllerCreds</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>KubeCloudControllerCreds is a reference to a secret containing cloud
credentials with permissions matching the cloud controller policy. The
secret should have exactly one key, <code>credentials</code>, whose value is an AWS
credentials file.</p>
<p>TODO(dan): document the &ldquo;cloud controller policy&rdquo;</p>
</td>
</tr>
<tr>
<td>
<code>nodePoolManagementCreds</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>NodePoolManagementCreds is a reference to a secret containing cloud
credentials with permissions matching the node pool management policy. The
secret should have exactly one key, <code>credentials</code>, whose value is an AWS
credentials file.</p>
<p>TODO(dan): document the &ldquo;node pool management policy&rdquo;</p>
</td>
</tr>
<tr>
<td>
<code>controlPlaneOperatorCreds</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>ControlPlaneOperatorCreds is a reference to a secret containing cloud
credentials with permissions matching the control-plane-operator policy.
The secret should have exactly one key, <code>credentials</code>, whose value is
an AWS credentials file.</p>
<p>TODO(dan): document the &ldquo;node pool management policy&rdquo;</p>
</td>
</tr>
<tr>
<td>
<code>resourceTags</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSResourceTag">
[]AWSResourceTag
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ResourceTags is a list of additional tags to apply to AWS resources created
for the cluster. See
<a href="https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html">https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html</a> for
information on tagging AWS resources. AWS supports a maximum of 50 tags per
resource. OpenShift reserves 25 tags for its use, leaving 25 tags available
for the user.</p>
</td>
</tr>
<tr>
<td>
<code>endpointAccess</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSEndpointAccessType">
AWSEndpointAccessType
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>EndpointAccess specifies the publishing scope of cluster endpoints. The
default is Public.</p>
<p>
Value must be one of:
&#34;Private&#34;, 
&#34;Public&#34;, 
&#34;PublicAndPrivate&#34;
</p>
</td>
</tr>
</tbody>
</table>
###AWSResourceReference { #hypershift.openshift.io/v1alpha1.AWSResourceReference }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSCloudProviderConfig">AWSCloudProviderConfig</a>, 
<a href="#hypershift.openshift.io/v1alpha1.AWSNodePoolPlatform">AWSNodePoolPlatform</a>)
</p>
<p>
<p>AWSResourceReference is a reference to a specific AWS resource by ID, ARN, or filters.
Only one of ID, ARN or Filters may be specified. Specifying more than one will result in
a validation error.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>id</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>ID of resource</p>
</td>
</tr>
<tr>
<td>
<code>arn</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>ARN of resource</p>
</td>
</tr>
<tr>
<td>
<code>filters</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.Filter">
[]Filter
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Filters is a set of key/value pairs used to identify a resource
They are applied according to the rules defined by the AWS API:
<a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Filtering.html">https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Filtering.html</a></p>
</td>
</tr>
</tbody>
</table>
###AWSResourceTag { #hypershift.openshift.io/v1alpha1.AWSResourceTag }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSNodePoolPlatform">AWSNodePoolPlatform</a>, 
<a href="#hypershift.openshift.io/v1alpha1.AWSPlatformSpec">AWSPlatformSpec</a>)
</p>
<p>
<p>AWSResourceTag is a tag to apply to AWS resources created for the cluster.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>key</code></br>
<em>
string
</em>
</td>
<td>
<p>Key is the key of the tag.</p>
</td>
</tr>
<tr>
<td>
<code>value</code></br>
<em>
string
</em>
</td>
<td>
<p>Value is the value of the tag.</p>
<p>Some AWS service do not support empty values. Since tags are added to
resources in many services, the length of the tag value must meet the
requirements of all services.</p>
</td>
</tr>
</tbody>
</table>
###AWSRoleCredentials { #hypershift.openshift.io/v1alpha1.AWSRoleCredentials }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSPlatformSpec">AWSPlatformSpec</a>)
</p>
<p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>arn</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>namespace</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>name</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
</tbody>
</table>
###AWSServiceEndpoint { #hypershift.openshift.io/v1alpha1.AWSServiceEndpoint }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSPlatformSpec">AWSPlatformSpec</a>)
</p>
<p>
<p>AWSServiceEndpoint stores the configuration for services to
override existing defaults of AWS Services.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>name</code></br>
<em>
string
</em>
</td>
<td>
<p>Name is the name of the AWS service.
This must be provided and cannot be empty.</p>
</td>
</tr>
<tr>
<td>
<code>url</code></br>
<em>
string
</em>
</td>
<td>
<p>URL is fully qualified URI with scheme https, that overrides the default generated
endpoint for a client.
This must be provided and cannot be empty.</p>
</td>
</tr>
</tbody>
</table>
###AvailabilityPolicy { #hypershift.openshift.io/v1alpha1.AvailabilityPolicy }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>AvailabilityPolicy specifies a high level availability policy for components.</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;HighlyAvailable&#34;</p></td>
<td><p>HighlyAvailable means components should be resilient to problems across
fault boundaries as defined by the component to which the policy is
attached. This usually means running critical workloads with 3 replicas and
with little or no toleration of disruption of the component.</p>
</td>
</tr><tr><td><p>&#34;SingleReplica&#34;</p></td>
<td><p>SingleReplica means components are not expected to be resilient to problems
across most fault boundaries associated with high availability. This
usually means running critical workloads with just 1 replica and with
toleration of full disruption of the component.</p>
</td>
</tr></tbody>
</table>
###ClusterAutoscaling { #hypershift.openshift.io/v1alpha1.ClusterAutoscaling }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>)
</p>
<p>
<p>ClusterAutoscaling specifies auto-scaling behavior that applies to all
NodePools associated with a control plane.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>maxNodesTotal</code></br>
<em>
int32
</em>
</td>
<td>
<p>MaxNodesTotal is the maximum allowable number of nodes across all NodePools
for a HostedCluster. The autoscaler will not grow the cluster beyond this
number.</p>
</td>
</tr>
<tr>
<td>
<code>maxPodGracePeriod</code></br>
<em>
int32
</em>
</td>
<td>
<p>MaxPodGracePeriod is the maximum seconds to wait for graceful pod
termination before scaling down a NodePool. The default is 600 seconds.</p>
</td>
</tr>
<tr>
<td>
<code>maxNodeProvisionTime</code></br>
<em>
string
</em>
</td>
<td>
<p>MaxNodeProvisionTime is the maximum time to wait for node provisioning
before considering the provisioning to be unsuccessful, expressed as a Go
duration string. The default is 15 minutes.</p>
</td>
</tr>
<tr>
<td>
<code>podPriorityThreshold</code></br>
<em>
int32
</em>
</td>
<td>
<em>(Optional)</em>
<p>PodPriorityThreshold enables users to schedule &ldquo;best-effort&rdquo; pods, which
shouldn&rsquo;t trigger autoscaler actions, but only run when there are spare
resources available. The default is -10.</p>
<p>See the following for more details:
<a href="https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-cluster-autoscaler-work-with-pod-priority-and-preemption">https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-cluster-autoscaler-work-with-pod-priority-and-preemption</a></p>
</td>
</tr>
</tbody>
</table>
###ClusterConfiguration { #hypershift.openshift.io/v1alpha1.ClusterConfiguration }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>ClusterConfiguration specifies configuration for individual OCP components in the
cluster, represented as embedded resources that correspond to the openshift
configuration API.</p>
<p>The API for individual configuration items is at:
<a href="https://docs.openshift.com/container-platform/4.7/rest_api/config_apis/config-apis-index.html">https://docs.openshift.com/container-platform/4.7/rest_api/config_apis/config-apis-index.html</a></p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>secretRefs</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
[]Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>SecretRefs holds references to any secrets referenced by configuration
entries. Entries can reference the secrets using local object references.</p>
</td>
</tr>
<tr>
<td>
<code>configMapRefs</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
[]Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ConfigMapRefs holds references to any configmaps referenced by
configuration entries. Entries can reference the configmaps using local
object references.</p>
</td>
</tr>
<tr>
<td>
<code>items</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#rawextension-runtime-pkg">
[]k8s.io/apimachinery/pkg/runtime.RawExtension
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Items embeds the serialized configuration resources.</p>
</td>
</tr>
</tbody>
</table>
###ClusterNetworking { #hypershift.openshift.io/v1alpha1.ClusterNetworking }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>)
</p>
<p>
<p>ClusterNetworking specifies network configuration for a cluster.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>serviceCIDR</code></br>
<em>
string
</em>
</td>
<td>
<p>ServiceCIDR is&hellip;</p>
<p>TODO(dan): document it</p>
</td>
</tr>
<tr>
<td>
<code>podCIDR</code></br>
<em>
string
</em>
</td>
<td>
<p>PodCIDR is&hellip;</p>
<p>TODO(dan): document it</p>
</td>
</tr>
<tr>
<td>
<code>machineCIDR</code></br>
<em>
string
</em>
</td>
<td>
<p>MachineCIDR is&hellip;</p>
<p>TODO(dan): document it</p>
</td>
</tr>
<tr>
<td>
<code>networkType</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NetworkType">
NetworkType
</a>
</em>
</td>
<td>
<p>NetworkType specifies the SDN provider used for cluster networking.</p>
<p>
Value must be one of:
&#34;Calico&#34;, 
&#34;OpenShiftSDN&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>apiServer</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.APIServerNetworking">
APIServerNetworking
</a>
</em>
</td>
<td>
<p>APIServer contains advanced network settings for the API server that affect
how the APIServer is exposed inside a cluster node.</p>
</td>
</tr>
</tbody>
</table>
###ClusterVersionStatus { #hypershift.openshift.io/v1alpha1.ClusterVersionStatus }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterStatus">HostedClusterStatus</a>)
</p>
<p>
<p>ClusterVersionStatus reports the status of the cluster versioning,
including any upgrades that are in progress. The current field will
be set to whichever version the cluster is reconciling to, and the
conditions array will report whether the update succeeded, is in
progress, or is failing.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>desired</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.Release">
Release
</a>
</em>
</td>
<td>
<p>desired is the version that the cluster is reconciling towards.
If the cluster is not yet fully initialized desired will be set
with the information available, which may be an image or a tag.</p>
</td>
</tr>
<tr>
<td>
<code>history</code></br>
<em>
[]github.com/openshift/api/config/v1.UpdateHistory
</em>
</td>
<td>
<em>(Optional)</em>
<p>history contains a list of the most recent versions applied to the cluster.
This value may be empty during cluster startup, and then will be updated
when a new update is being applied. The newest update is first in the
list and it is ordered by recency. Updates in the history have state
Completed if the rollout completed - if an update was failing or halfway
applied the state will be Partial. Only a limited amount of update history
is preserved.</p>
</td>
</tr>
<tr>
<td>
<code>observedGeneration</code></br>
<em>
int64
</em>
</td>
<td>
<p>observedGeneration reports which version of the spec is being synced.
If this value is not equal to metadata.generation, then the desired
and conditions fields may represent a previous version.</p>
</td>
</tr>
</tbody>
</table>
###ConditionType { #hypershift.openshift.io/v1alpha1.ConditionType }
<p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;EndpointAvailable&#34;</p></td>
<td><p>AWSEndpointServiceAvailable indicates whether the AWS Endpoint has been
created in the guest VPC</p>
</td>
</tr><tr><td><p>&#34;EndpointServiceAvailable&#34;</p></td>
<td><p>AWSEndpointServiceAvailable indicates whether the AWS Endpoint Service
has been created for the specified NLB in the management VPC</p>
</td>
</tr><tr><td><p>&#34;ClusterVersionFailing&#34;</p></td>
<td></td>
</tr><tr><td><p>&#34;EtcdAvailable&#34;</p></td>
<td></td>
</tr><tr><td><p>&#34;Available&#34;</p></td>
<td><p>HostedClusterAvailable indicates whether the HostedCluster has a healthy
control plane.</p>
</td>
</tr><tr><td><p>&#34;Available&#34;</p></td>
<td></td>
</tr><tr><td><p>&#34;IgnitionEndpointAvailable&#34;</p></td>
<td><p>IgnitionEndpointAvailable indicates whether the ignition server for the
HostedCluster is available to handle ignition requests.</p>
</td>
</tr><tr><td><p>&#34;InfrastructureReady&#34;</p></td>
<td></td>
</tr><tr><td><p>&#34;KubeAPIServerAvailable&#34;</p></td>
<td></td>
</tr><tr><td><p>&#34;SupportedHostedCluster&#34;</p></td>
<td><p>SupportedHostedCluster indicates whether a HostedCluster is supported by
the current configuration of the hypershift-operator.
e.g. If HostedCluster requests endpointAcess Private but the hypershift-operator
is running on a management cluster outside AWS or is not configured with AWS
credentials, the HostedCluster is not supported.</p>
</td>
</tr><tr><td><p>&#34;UnmanagedEtcdAvailable&#34;</p></td>
<td><p>UnmanagedEtcdAvailable indicates whether a user-managed etcd cluster is
healthy.</p>
</td>
</tr><tr><td><p>&#34;ValidConfiguration&#34;</p></td>
<td><p>ValidHostedClusterConfiguration indicates (if status is true) that the
ClusterConfiguration specified for the HostedCluster is valid.</p>
</td>
</tr><tr><td><p>&#34;ValidHostedControlPlaneConfiguration&#34;</p></td>
<td></td>
</tr></tbody>
</table>
###DNSSpec { #hypershift.openshift.io/v1alpha1.DNSSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>DNSSpec specifies the DNS configuration in the cluster.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>baseDomain</code></br>
<em>
string
</em>
</td>
<td>
<p>BaseDomain is the base domain of the cluster.</p>
</td>
</tr>
<tr>
<td>
<code>publicZoneID</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>PublicZoneID is the Hosted Zone ID where all the DNS records that are
publicly accessible to the internet exist.</p>
</td>
</tr>
<tr>
<td>
<code>privateZoneID</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>PrivateZoneID is the Hosted Zone ID where all the DNS records that are only
available internally to the cluster exist.</p>
</td>
</tr>
</tbody>
</table>
###EtcdManagementType { #hypershift.openshift.io/v1alpha1.EtcdManagementType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.EtcdSpec">EtcdSpec</a>)
</p>
<p>
<p>EtcdManagementType is a enum specifying the strategy for managing the cluster&rsquo;s etcd instance</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;Managed&#34;</p></td>
<td><p>Managed means HyperShift should provision and operator the etcd cluster
automatically.</p>
</td>
</tr><tr><td><p>&#34;Unmanaged&#34;</p></td>
<td><p>Unmanaged means HyperShift will not provision or manage the etcd cluster,
and the user is responsible for doing so.</p>
</td>
</tr></tbody>
</table>
###EtcdSpec { #hypershift.openshift.io/v1alpha1.EtcdSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>EtcdSpec specifies configuration for a control plane etcd cluster.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>managementType</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.EtcdManagementType">
EtcdManagementType
</a>
</em>
</td>
<td>
<p>ManagementType defines how the etcd cluster is managed.</p>
<p>
Value must be one of:
&#34;Managed&#34;, 
&#34;Unmanaged&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>managed</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ManagedEtcdSpec">
ManagedEtcdSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Managed specifies the behavior of an etcd cluster managed by HyperShift.</p>
</td>
</tr>
<tr>
<td>
<code>unmanaged</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.UnmanagedEtcdSpec">
UnmanagedEtcdSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Unmanaged specifies configuration which enables the control plane to
integrate with an eternally managed etcd cluster.</p>
</td>
</tr>
</tbody>
</table>
###EtcdTLSConfig { #hypershift.openshift.io/v1alpha1.EtcdTLSConfig }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.UnmanagedEtcdSpec">UnmanagedEtcdSpec</a>)
</p>
<p>
<p>EtcdTLSConfig specifies TLS configuration for HTTPS etcd client endpoints.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>clientSecret</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>ClientSecret refers to a secret for client mTLS authentication with the etcd cluster. It
may have the following key/value pairs:</p>
<pre><code>etcd-client-ca.crt: Certificate Authority value
etcd-client.crt: Client certificate value
etcd-client.key: Client certificate key value
</code></pre>
</td>
</tr>
</tbody>
</table>
###Filter { #hypershift.openshift.io/v1alpha1.Filter }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSResourceReference">AWSResourceReference</a>)
</p>
<p>
<p>Filter is a filter used to identify an AWS resource</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>name</code></br>
<em>
string
</em>
</td>
<td>
<p>Name of the filter. Filter names are case-sensitive.</p>
</td>
</tr>
<tr>
<td>
<code>values</code></br>
<em>
[]string
</em>
</td>
<td>
<p>Values includes one or more filter values. Filter values are case-sensitive.</p>
</td>
</tr>
</tbody>
</table>
###HostedClusterSpec { #hypershift.openshift.io/v1alpha1.HostedClusterSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedCluster">HostedCluster</a>)
</p>
<p>
<p>HostedClusterSpec is the desired behavior of a HostedCluster.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>release</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.Release">
Release
</a>
</em>
</td>
<td>
<p>Release specifies the desired OCP release payload for the hosted cluster.</p>
<p>Updating this field will trigger a rollout of the control plane. The
behavior of the rollout will be driven by the ControllerAvailabilityPolicy
and InfrastructureAvailabilityPolicy.</p>
</td>
</tr>
<tr>
<td>
<code>infraID</code></br>
<em>
string
</em>
</td>
<td>
<p>InfraID is a globally unique identifier for the cluster. This identifier
will be used to associate various cloud resources with the HostedCluster
and its associated NodePools.</p>
<p>TODO(dan): consider moving this to .platform.aws.infraID</p>
</td>
</tr>
<tr>
<td>
<code>platform</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.PlatformSpec">
PlatformSpec
</a>
</em>
</td>
<td>
<p>Platform specifies the underlying infrastructure provider for the cluster
and is used to configure platform specific behavior.</p>
</td>
</tr>
<tr>
<td>
<code>controllerAvailabilityPolicy</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AvailabilityPolicy">
AvailabilityPolicy
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ControllerAvailabilityPolicy specifies the availability policy applied to
critical control plane components. The default value is SingleReplica.</p>
<p>
Value must be one of:
&#34;HighlyAvailable&#34;, 
&#34;SingleReplica&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>infrastructureAvailabilityPolicy</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AvailabilityPolicy">
AvailabilityPolicy
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>InfrastructureAvailabilityPolicy specifies the availability policy applied
to infrastructure services which run on cluster nodes. The default value is
HighlyAvailable.</p>
<p>
Value must be one of:
&#34;HighlyAvailable&#34;, 
&#34;SingleReplica&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>dns</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.DNSSpec">
DNSSpec
</a>
</em>
</td>
<td>
<p>DNS specifies DNS configuration for the cluster.</p>
</td>
</tr>
<tr>
<td>
<code>networking</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterNetworking">
ClusterNetworking
</a>
</em>
</td>
<td>
<p>Networking specifies network configuration for the cluster.</p>
</td>
</tr>
<tr>
<td>
<code>autoscaling</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterAutoscaling">
ClusterAutoscaling
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Autoscaling specifies auto-scaling behavior that applies to all NodePools
associated with the control plane.</p>
</td>
</tr>
<tr>
<td>
<code>etcd</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.EtcdSpec">
EtcdSpec
</a>
</em>
</td>
<td>
<p>Etcd specifies configuration for the control plane etcd cluster. The
default ManagementType is Managed. Once set, the ManagementType cannot be
changed.</p>
</td>
</tr>
<tr>
<td>
<code>services</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ServicePublishingStrategyMapping">
[]ServicePublishingStrategyMapping
</a>
</em>
</td>
<td>
<p>Services specifies how individual control plane services are published from
the hosting cluster of the control plane.</p>
<p>If a given service is not present in this list, it will be exposed publicly
by default.</p>
</td>
</tr>
<tr>
<td>
<code>pullSecret</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>PullSecret references a pull secret to be injected into the container
runtime of all cluster nodes. The secret must have a key named
&ldquo;.dockerconfigjson&rdquo; whose value is the pull secret JSON.</p>
</td>
</tr>
<tr>
<td>
<code>sshKey</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>SSHKey references an SSH key to be injected into all cluster node sshd
servers. The secret must have a single key &ldquo;id_rsa.pub&rdquo; whose value is the
public part of an SSH key.</p>
</td>
</tr>
<tr>
<td>
<code>issuerURL</code></br>
<em>
string
</em>
</td>
<td>
<p>IssuerURL is an OIDC issuer URL which is used as the issuer in all
ServiceAccount tokens generated by the control plane API server. The
default value is kubernetes.default.svc, which only works for in-cluster
validation.</p>
</td>
</tr>
<tr>
<td>
<code>configuration</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterConfiguration">
ClusterConfiguration
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Configuration specifies configuration for individual OCP components in the
cluster, represented as embedded resources that correspond to the openshift
configuration API.</p>
</td>
</tr>
<tr>
<td>
<code>auditWebhook</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>AuditWebhook contains metadata for configuring an audit webhook endpoint
for a cluster to process cluster audit events. It references a secret that
contains the webhook information for the audit webhook endpoint. It is a
secret because if the endpoint has mTLS the kubeconfig will contain client
keys. The kubeconfig needs to be stored in the secret with a secret key
name that corresponds to the constant AuditWebhookKubeconfigKey.</p>
<p>This field is currently only supported on the IBMCloud platform.</p>
</td>
</tr>
<tr>
<td>
<code>imageContentSources</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ImageContentSource">
[]ImageContentSource
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ImageContentSources specifies image mirrors that can be used by cluster
nodes to pull content.</p>
</td>
</tr>
<tr>
<td>
<code>secretEncryption</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.SecretEncryptionSpec">
SecretEncryptionSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>SecretEncryption specifies a Kubernetes secret encryption strategy for the
control plane.</p>
</td>
</tr>
<tr>
<td>
<code>fips</code></br>
<em>
bool
</em>
</td>
<td>
<em>(Optional)</em>
<p>FIPS indicates whether this cluster&rsquo;s nodes will be running in FIPS mode.
If set to true, the control plane&rsquo;s ignition server will be configured to
expect that nodes joining the cluster will be FIPS-enabled.</p>
</td>
</tr>
</tbody>
</table>
###HostedClusterStatus { #hypershift.openshift.io/v1alpha1.HostedClusterStatus }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedCluster">HostedCluster</a>)
</p>
<p>
<p>HostedClusterStatus is the latest observed status of a HostedCluster.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>version</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterVersionStatus">
ClusterVersionStatus
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Version is the status of the release version applied to the
HostedCluster.</p>
</td>
</tr>
<tr>
<td>
<code>kubeconfig</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>KubeConfig is a reference to the secret containing the default kubeconfig
for the cluster.</p>
</td>
</tr>
<tr>
<td>
<code>ignitionEndpoint</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>IgnitionEndpoint is the endpoint injected in the ign config userdata.
It exposes the config for instances to become kubernetes nodes.</p>
</td>
</tr>
<tr>
<td>
<code>conditions</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#condition-v1-meta">
[]Kubernetes meta/v1.Condition
</a>
</em>
</td>
<td>
<p>Conditions represents the latest available observations of a control
plane&rsquo;s current state.</p>
</td>
</tr>
</tbody>
</table>
###HostedControlPlaneSpec { #hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec }
<p>
<p>HostedControlPlaneSpec defines the desired state of HostedControlPlane</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>releaseImage</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>pullSecret</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>issuerURL</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>serviceCIDR</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>podCIDR</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>machineCIDR</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>networkType</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NetworkType">
NetworkType
</a>
</em>
</td>
<td>
<p>NetworkType specifies the SDN provider used for cluster networking.</p>
<p>
Value must be one of:
&#34;Calico&#34;, 
&#34;OpenShiftSDN&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>sshKey</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>infraID</code></br>
<em>
string
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>platform</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.PlatformSpec">
PlatformSpec
</a>
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>dns</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.DNSSpec">
DNSSpec
</a>
</em>
</td>
<td>
</td>
</tr>
<tr>
<td>
<code>apiPort</code></br>
<em>
int32
</em>
</td>
<td>
<em>(Optional)</em>
<p>APIPort is the port at which the APIServer listens inside a worker</p>
</td>
</tr>
<tr>
<td>
<code>apiAdvertiseAddress</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>APIAdvertiseAddress is the address at which the APIServer listens
inside a worker.</p>
</td>
</tr>
<tr>
<td>
<code>controllerAvailabilityPolicy</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AvailabilityPolicy">
AvailabilityPolicy
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ControllerAvailabilityPolicy specifies whether to run control plane controllers in HA mode
Defaults to SingleReplica when not set</p>
<p>
Value must be one of:
&#34;HighlyAvailable&#34;, 
&#34;SingleReplica&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>infrastructureAvailabilityPolicy</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AvailabilityPolicy">
AvailabilityPolicy
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>InfrastructureAvailabilityPolicy specifies whether to run infrastructure services that
run on the guest cluster nodes in HA mode
Defaults to HighlyAvailable when not set</p>
<p>
Value must be one of:
&#34;HighlyAvailable&#34;, 
&#34;SingleReplica&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>fips</code></br>
<em>
bool
</em>
</td>
<td>
<em>(Optional)</em>
<p>FIPS specifies if the nodes for the cluster will be running in FIPS mode</p>
</td>
</tr>
<tr>
<td>
<code>kubeconfig</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.KubeconfigSecretRef">
KubeconfigSecretRef
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>KubeConfig specifies the name and key for the kubeconfig secret</p>
</td>
</tr>
<tr>
<td>
<code>services</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ServicePublishingStrategyMapping">
[]ServicePublishingStrategyMapping
</a>
</em>
</td>
<td>
<p>Services defines metadata about how control plane services are published
in the management cluster.</p>
</td>
</tr>
<tr>
<td>
<code>auditWebhook</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>AuditWebhook contains metadata for configuring an audit webhook
endpoint for a cluster to process cluster audit events. It references
a secret that contains the webhook information for the audit webhook endpoint.
It is a secret because if the endpoint has MTLS the kubeconfig will contain client
keys. This is currently only supported in IBM Cloud. The kubeconfig needs to be stored
in the secret with a secret key name that corresponds to the constant AuditWebhookKubeconfigKey.</p>
</td>
</tr>
<tr>
<td>
<code>etcd</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.EtcdSpec">
EtcdSpec
</a>
</em>
</td>
<td>
<p>Etcd contains metadata about the etcd cluster the hypershift managed Openshift control plane components
use to store data.</p>
</td>
</tr>
<tr>
<td>
<code>configuration</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterConfiguration">
ClusterConfiguration
</a>
</em>
</td>
<td>
<p>Configuration embeds resources that correspond to the openshift configuration API:
<a href="https://docs.openshift.com/container-platform/4.7/rest_api/config_apis/config-apis-index.html">https://docs.openshift.com/container-platform/4.7/rest_api/config_apis/config-apis-index.html</a></p>
</td>
</tr>
<tr>
<td>
<code>imageContentSources</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ImageContentSource">
[]ImageContentSource
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>ImageContentSources lists sources/repositories for the release-image content.</p>
</td>
</tr>
<tr>
<td>
<code>secretEncryption</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.SecretEncryptionSpec">
SecretEncryptionSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>SecretEncryption contains metadata about the kubernetes secret encryption strategy being used for the
cluster when applicable.</p>
</td>
</tr>
</tbody>
</table>
###HostedControlPlaneStatus { #hypershift.openshift.io/v1alpha1.HostedControlPlaneStatus }
<p>
<p>HostedControlPlaneStatus defines the observed state of HostedControlPlane</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>ready</code></br>
<em>
bool
</em>
</td>
<td>
<p>Ready denotes that the HostedControlPlane API Server is ready to
receive requests
This satisfies CAPI contract <a href="https://github.com/kubernetes-sigs/cluster-api/blob/cd3a694deac89d5ebeb888307deaa61487207aa0/controllers/cluster_controller_phases.go#L226-L230">https://github.com/kubernetes-sigs/cluster-api/blob/cd3a694deac89d5ebeb888307deaa61487207aa0/controllers/cluster_controller_phases.go#L226-L230</a></p>
</td>
</tr>
<tr>
<td>
<code>initialized</code></br>
<em>
bool
</em>
</td>
<td>
<p>Initialized denotes whether or not the control plane has
provided a kubeadm-config.
Once this condition is marked true, its value is never changed. See the Ready condition for an indication of
the current readiness of the cluster&rsquo;s control plane.
This satisfies CAPI contract <a href="https://github.com/kubernetes-sigs/cluster-api/blob/cd3a694deac89d5ebeb888307deaa61487207aa0/controllers/cluster_controller_phases.go#L238-L252">https://github.com/kubernetes-sigs/cluster-api/blob/cd3a694deac89d5ebeb888307deaa61487207aa0/controllers/cluster_controller_phases.go#L238-L252</a></p>
</td>
</tr>
<tr>
<td>
<code>externalManagedControlPlane</code></br>
<em>
bool
</em>
</td>
<td>
<p>ExternalManagedControlPlane indicates to cluster-api that the control plane
is managed by an external service.
<a href="https://github.com/kubernetes-sigs/cluster-api/blob/65e5385bffd71bf4aad3cf34a537f11b217c7fab/controllers/machine_controller.go#L468">https://github.com/kubernetes-sigs/cluster-api/blob/65e5385bffd71bf4aad3cf34a537f11b217c7fab/controllers/machine_controller.go#L468</a></p>
</td>
</tr>
<tr>
<td>
<code>controlPlaneEndpoint</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.APIEndpoint">
APIEndpoint
</a>
</em>
</td>
<td>
<p>ControlPlaneEndpoint contains the endpoint information by which
external clients can access the control plane.  This is populated
after the infrastructure is ready.</p>
</td>
</tr>
<tr>
<td>
<code>version</code></br>
<em>
string
</em>
</td>
<td>
<p>Version is the semantic version of the release applied by
the hosted control plane operator</p>
</td>
</tr>
<tr>
<td>
<code>releaseImage</code></br>
<em>
string
</em>
</td>
<td>
<p>ReleaseImage is the release image applied to the hosted control plane.</p>
</td>
</tr>
<tr>
<td>
<code>lastReleaseImageTransitionTime</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#time-v1-meta">
Kubernetes meta/v1.Time
</a>
</em>
</td>
<td>
<p>lastReleaseImageTransitionTime is the time of the last update to the current
releaseImage property.</p>
</td>
</tr>
<tr>
<td>
<code>kubeConfig</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.KubeconfigSecretRef">
KubeconfigSecretRef
</a>
</em>
</td>
<td>
<p>KubeConfig is a reference to the secret containing the default kubeconfig
for this control plane.</p>
</td>
</tr>
<tr>
<td>
<code>conditions</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#condition-v1-meta">
[]Kubernetes meta/v1.Condition
</a>
</em>
</td>
<td>
<p>Condition contains details for one aspect of the current state of the HostedControlPlane.
Current condition types are: &ldquo;Available&rdquo;</p>
</td>
</tr>
</tbody>
</table>
###IBMCloudKMSAuthSpec { #hypershift.openshift.io/v1alpha1.IBMCloudKMSAuthSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSSpec">IBMCloudKMSSpec</a>)
</p>
<p>
<p>IBMCloudKMSAuthSpec defines metadata for how authentication is done with IBM Cloud KMS</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>type</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSAuthType">
IBMCloudKMSAuthType
</a>
</em>
</td>
<td>
<p>Type defines the IBM Cloud KMS authentication strategy</p>
<p>
Value must be one of:
&#34;Managed&#34;, 
&#34;Unmanaged&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>unmanaged</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSUnmanagedAuthSpec">
IBMCloudKMSUnmanagedAuthSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Unmanaged defines the auth metadata the customer provides to interact with IBM Cloud KMS</p>
</td>
</tr>
<tr>
<td>
<code>managed</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSManagedAuthSpec">
IBMCloudKMSManagedAuthSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Managed defines metadata around the service to service authentication strategy for the IBM Cloud
KMS system (all provider managed).</p>
</td>
</tr>
</tbody>
</table>
###IBMCloudKMSAuthType { #hypershift.openshift.io/v1alpha1.IBMCloudKMSAuthType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSAuthSpec">IBMCloudKMSAuthSpec</a>)
</p>
<p>
<p>IBMCloudKMSAuthType defines the IBM Cloud KMS authentication strategy</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;Managed&#34;</p></td>
<td><p>IBMCloudKMSManagedAuth defines the KMS authentication strategy where the IKS/ROKS platform uses
service to service auth to call IBM Cloud KMS APIs (no customer credentials requried)</p>
</td>
</tr><tr><td><p>&#34;Unmanaged&#34;</p></td>
<td><p>IBMCloudKMSUnmanagedAuth defines the KMS authentication strategy where a customer supplies IBM Cloud
authentication to interact with IBM Cloud KMS APIs</p>
</td>
</tr></tbody>
</table>
###IBMCloudKMSKeyEntry { #hypershift.openshift.io/v1alpha1.IBMCloudKMSKeyEntry }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSSpec">IBMCloudKMSSpec</a>)
</p>
<p>
<p>IBMCloudKMSKeyEntry defines metadata for an IBM Cloud KMS encryption key</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>crkID</code></br>
<em>
string
</em>
</td>
<td>
<p>CRKID is the customer rook key id</p>
</td>
</tr>
<tr>
<td>
<code>instanceID</code></br>
<em>
string
</em>
</td>
<td>
<p>InstanceID is the id for the key protect instance</p>
</td>
</tr>
<tr>
<td>
<code>correlationID</code></br>
<em>
string
</em>
</td>
<td>
<p>CorrelationID is an identifier used to track all api call usage from hypershift</p>
</td>
</tr>
<tr>
<td>
<code>url</code></br>
<em>
string
</em>
</td>
<td>
<p>URL is the url to call key protect apis over</p>
</td>
</tr>
<tr>
<td>
<code>keyVersion</code></br>
<em>
int
</em>
</td>
<td>
<p>KeyVersion is a unique number associated with the key. The number increments whenever a new
key is enabled for data encryption.</p>
</td>
</tr>
</tbody>
</table>
###IBMCloudKMSManagedAuthSpec { #hypershift.openshift.io/v1alpha1.IBMCloudKMSManagedAuthSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSAuthSpec">IBMCloudKMSAuthSpec</a>)
</p>
<p>
<p>IBMCloudKMSManagedAuthSpec defines metadata around the service to service authentication strategy for the IBM Cloud
KMS system (all provider managed).</p>
</p>
###IBMCloudKMSSpec { #hypershift.openshift.io/v1alpha1.IBMCloudKMSSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.KMSSpec">KMSSpec</a>)
</p>
<p>
<p>IBMCloudKMSSpec defines metadata for the IBM Cloud KMS encryption strategy</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>region</code></br>
<em>
string
</em>
</td>
<td>
<p>Region is the IBM Cloud region</p>
</td>
</tr>
<tr>
<td>
<code>auth</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSAuthSpec">
IBMCloudKMSAuthSpec
</a>
</em>
</td>
<td>
<p>Auth defines metadata for how authentication is done with IBM Cloud KMS</p>
</td>
</tr>
<tr>
<td>
<code>keyList</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSKeyEntry">
[]IBMCloudKMSKeyEntry
</a>
</em>
</td>
<td>
<p>KeyList defines the list of keys used for data encryption</p>
</td>
</tr>
</tbody>
</table>
###IBMCloudKMSUnmanagedAuthSpec { #hypershift.openshift.io/v1alpha1.IBMCloudKMSUnmanagedAuthSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSAuthSpec">IBMCloudKMSAuthSpec</a>)
</p>
<p>
<p>IBMCloudKMSUnmanagedAuthSpec defines the auth metadata the customer provides to interact with IBM Cloud KMS</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>credentials</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>Credentials should reference a secret with a key field of IBMCloudIAMAPIKeySecretKey that contains a apikey to
call IBM Cloud KMS APIs</p>
</td>
</tr>
</tbody>
</table>
###ImageContentSource { #hypershift.openshift.io/v1alpha1.ImageContentSource }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>ImageContentSource specifies image mirrors that can be used by cluster nodes
to pull content. For cluster workloads, if a container image registry host of
the pullspec matches Source then one of the Mirrors are substituted as hosts
in the pullspec and tried in order to fetch the image.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>source</code></br>
<em>
string
</em>
</td>
<td>
<p>Source is the repository that users refer to, e.g. in image pull
specifications.</p>
</td>
</tr>
<tr>
<td>
<code>mirrors</code></br>
<em>
[]string
</em>
</td>
<td>
<em>(Optional)</em>
<p>Mirrors are one or more repositories that may also contain the same images.</p>
</td>
</tr>
</tbody>
</table>
###InPlaceUpgrade { #hypershift.openshift.io/v1alpha1.InPlaceUpgrade }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolManagement">NodePoolManagement</a>)
</p>
<p>
<p>InPlaceUpgrade specifies an upgrade strategy which upgrades nodes in-place
without any new nodes being created or any old nodes being deleted.</p>
</p>
###KMSProvider { #hypershift.openshift.io/v1alpha1.KMSProvider }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.KMSSpec">KMSSpec</a>)
</p>
<p>
<p>KMSProvider defines the supported KMS providers</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;AWS&#34;</p></td>
<td></td>
</tr><tr><td><p>&#34;IBMCloud&#34;</p></td>
<td></td>
</tr></tbody>
</table>
###KMSSpec { #hypershift.openshift.io/v1alpha1.KMSSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.SecretEncryptionSpec">SecretEncryptionSpec</a>)
</p>
<p>
<p>KMSSpec defines metadata about the kms secret encryption strategy</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>provider</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.KMSProvider">
KMSProvider
</a>
</em>
</td>
<td>
<p>Provider defines the KMS provider</p>
<p>
Value must be one of:
&#34;AWS&#34;, 
&#34;IBMCloud&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>ibmcloud</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.IBMCloudKMSSpec">
IBMCloudKMSSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>IBMCloud defines metadata for the IBM Cloud KMS encryption strategy</p>
</td>
</tr>
<tr>
<td>
<code>aws</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSKMSSpec">
AWSKMSSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>AWS defines metadata about the configuration of the AWS KMS Secret Encryption provider</p>
</td>
</tr>
</tbody>
</table>
###ManagedEtcdSpec { #hypershift.openshift.io/v1alpha1.ManagedEtcdSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.EtcdSpec">EtcdSpec</a>)
</p>
<p>
<p>ManagedEtcdSpec specifies the behavior of an etcd cluster managed by
HyperShift.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>storage</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ManagedEtcdStorageSpec">
ManagedEtcdStorageSpec
</a>
</em>
</td>
<td>
<p>Storage specifies how etcd data is persisted.</p>
</td>
</tr>
</tbody>
</table>
###ManagedEtcdStorageSpec { #hypershift.openshift.io/v1alpha1.ManagedEtcdStorageSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ManagedEtcdSpec">ManagedEtcdSpec</a>)
</p>
<p>
<p>ManagedEtcdStorageSpec describes the storage configuration for etcd data.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>type</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ManagedEtcdStorageType">
ManagedEtcdStorageType
</a>
</em>
</td>
<td>
<p>Type is the kind of persistent storage implementation to use for etcd.</p>
<p>
Value must be one of:
&#34;PersistentVolume&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>persistentVolume</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.PersistentVolumeEtcdStorageSpec">
PersistentVolumeEtcdStorageSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>PersistentVolume is the configuration for PersistentVolume etcd storage.
With this implementation, a PersistentVolume will be allocated for every
etcd member (either 1 or 3 depending on the HostedCluster control plane
availability configuration).</p>
</td>
</tr>
</tbody>
</table>
###ManagedEtcdStorageType { #hypershift.openshift.io/v1alpha1.ManagedEtcdStorageType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ManagedEtcdStorageSpec">ManagedEtcdStorageSpec</a>)
</p>
<p>
<p>ManagedEtcdStorageType is a storage type for an etcd cluster.</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;PersistentVolume&#34;</p></td>
<td><p>PersistentVolumeEtcdStorage uses PersistentVolumes for etcd storage.</p>
</td>
</tr></tbody>
</table>
###NetworkType { #hypershift.openshift.io/v1alpha1.NetworkType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterNetworking">ClusterNetworking</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>NetworkType specifies the SDN provider used for cluster networking.</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;Calico&#34;</p></td>
<td><p>Calico specifies Calico as the SDN provider</p>
</td>
</tr><tr><td><p>&#34;OpenShiftSDN&#34;</p></td>
<td><p>OpenShiftSDN specifies OpenshiftSDN as the SDN provider</p>
</td>
</tr></tbody>
</table>
###NodePoolAutoScaling { #hypershift.openshift.io/v1alpha1.NodePoolAutoScaling }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolSpec">NodePoolSpec</a>)
</p>
<p>
<p>NodePoolAutoScaling specifies auto-scaling behavior for a NodePool.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>min</code></br>
<em>
int32
</em>
</td>
<td>
<p>Min is the minimum number of nodes to maintain in the pool. Must be &gt;= 1.</p>
</td>
</tr>
<tr>
<td>
<code>max</code></br>
<em>
int32
</em>
</td>
<td>
<p>Max is the maximum number of nodes allowed in the pool. Must be &gt;= 1.</p>
</td>
</tr>
</tbody>
</table>
###NodePoolManagement { #hypershift.openshift.io/v1alpha1.NodePoolManagement }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolSpec">NodePoolSpec</a>)
</p>
<p>
<p>NodePoolManagement specifies behavior for managing nodes in a NodePool, such
as upgrade strategies and auto-repair behaviors.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>upgradeType</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.UpgradeType">
UpgradeType
</a>
</em>
</td>
<td>
<p>UpgradeType specifies the type of strategy for handling upgrades.</p>
<p>
Value must be one of:
&#34;InPlace&#34;, 
&#34;Replace&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>replace</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ReplaceUpgrade">
ReplaceUpgrade
</a>
</em>
</td>
<td>
<p>Replace is the configuration for rolling upgrades.</p>
</td>
</tr>
<tr>
<td>
<code>inPlace</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.InPlaceUpgrade">
InPlaceUpgrade
</a>
</em>
</td>
<td>
<p>InPlace is the configuration for in-place upgrades.</p>
</td>
</tr>
<tr>
<td>
<code>autoRepair</code></br>
<em>
bool
</em>
</td>
<td>
<em>(Optional)</em>
<p>AutoRepair specifies whether health checks should be enabled for machines
in the NodePool. The default is false.</p>
</td>
</tr>
</tbody>
</table>
###NodePoolPlatform { #hypershift.openshift.io/v1alpha1.NodePoolPlatform }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolSpec">NodePoolSpec</a>)
</p>
<p>
<p>NodePoolPlatform specifies the underlying infrastructure provider for the
NodePool and is used to configure platform specific behavior.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>type</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.PlatformType">
PlatformType
</a>
</em>
</td>
<td>
<p>Type specifies the platform name.</p>
<p>
Value must be one of:
&#34;AWS&#34;, 
&#34;IBMCloud&#34;, 
&#34;None&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>aws</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSNodePoolPlatform">
AWSNodePoolPlatform
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>AWS specifies the configuration used when operating on AWS.</p>
</td>
</tr>
</tbody>
</table>
###NodePoolSpec { #hypershift.openshift.io/v1alpha1.NodePoolSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePool">NodePool</a>)
</p>
<p>
<p>NodePoolSpec is the desired behavior of a NodePool.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>clusterName</code></br>
<em>
string
</em>
</td>
<td>
<p>ClusterName is the name of the HostedCluster this NodePool belongs to.</p>
<p>TODO(dan): Should this be a LocalObjectReference?</p>
</td>
</tr>
<tr>
<td>
<code>release</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.Release">
Release
</a>
</em>
</td>
<td>
<p>Release specifies the OCP release used for the NodePool. This informs the
ignition configuration for machines, as well as other platform specific
machine properties (e.g. an AMI on the AWS platform).</p>
</td>
</tr>
<tr>
<td>
<code>platform</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolPlatform">
NodePoolPlatform
</a>
</em>
</td>
<td>
<p>Platform specifies the underlying infrastructure provider for the NodePool
and is used to configure platform specific behavior.</p>
</td>
</tr>
<tr>
<td>
<code>nodeCount</code></br>
<em>
int32
</em>
</td>
<td>
<em>(Optional)</em>
<p>NodeCount is the desired number of nodes the pool should maintain. If
unset, the default value is 0.</p>
</td>
</tr>
<tr>
<td>
<code>management</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolManagement">
NodePoolManagement
</a>
</em>
</td>
<td>
<p>Management specifies behavior for managing nodes in the pool, such as
upgrade strategies and auto-repair behaviors.</p>
</td>
</tr>
<tr>
<td>
<code>autoScaling</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolAutoScaling">
NodePoolAutoScaling
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Autoscaling specifies auto-scaling behavior for the NodePool.</p>
</td>
</tr>
<tr>
<td>
<code>config</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#localobjectreference-v1-core">
[]Kubernetes core/v1.LocalObjectReference
</a>
</em>
</td>
<td>
<p>Config is a list of references to ConfigMaps containing serialized
MachineConfig resources to be injected into the ignition configurations of
nodes in the NodePool. The MachineConfig API schema is defined here:</p>
<p><a href="https://github.com/openshift/machine-config-operator/blob/master/pkg/apis/machineconfiguration.openshift.io/v1/types.go#L172">https://github.com/openshift/machine-config-operator/blob/master/pkg/apis/machineconfiguration.openshift.io/v1/types.go#L172</a></p>
<p>Each ConfigMap must have a single key named &ldquo;config&rdquo; whose value is the
JSON or YAML of a serialized MachineConfig.</p>
<p>TODO (alberto): this ConfigMaps are meant to contain MachineConfig,
KubeletConfig and ContainerRuntimeConfig but MCO only supports
MachineConfig in bootstrap mode atm. See:
<a href="https://github.com/openshift/machine-config-operator/blob/9c6c2bfd7ed498bfbc296d530d1839bd6a177b0b/pkg/controller/bootstrap/bootstrap.go#L104-L119">https://github.com/openshift/machine-config-operator/blob/9c6c2bfd7ed498bfbc296d530d1839bd6a177b0b/pkg/controller/bootstrap/bootstrap.go#L104-L119</a></p>
</td>
</tr>
</tbody>
</table>
###NodePoolStatus { #hypershift.openshift.io/v1alpha1.NodePoolStatus }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePool">NodePool</a>)
</p>
<p>
<p>NodePoolStatus is the latest observed status of a NodePool.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>nodeCount</code></br>
<em>
int32
</em>
</td>
<td>
<em>(Optional)</em>
<p>NodeCount is the latest observed number of nodes in the pool.</p>
</td>
</tr>
<tr>
<td>
<code>version</code></br>
<em>
string
</em>
</td>
<td>
<p>Version is the semantic version of the latest applied release specified by
the NodePool.</p>
</td>
</tr>
<tr>
<td>
<code>conditions</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#condition-v1-meta">
[]Kubernetes meta/v1.Condition
</a>
</em>
</td>
<td>
<p>Conditions represents the latest available observations of the node pool&rsquo;s
current state.</p>
</td>
</tr>
</tbody>
</table>
###NodePortPublishingStrategy { #hypershift.openshift.io/v1alpha1.NodePortPublishingStrategy }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ServicePublishingStrategy">ServicePublishingStrategy</a>)
</p>
<p>
<p>NodePortPublishingStrategy specifies a NodePort used to expose a service.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>address</code></br>
<em>
string
</em>
</td>
<td>
<p>Address is the host/ip that the NodePort service is exposed over.</p>
</td>
</tr>
<tr>
<td>
<code>port</code></br>
<em>
int32
</em>
</td>
<td>
<p>Port is the port of the NodePort service. If &lt;=0, the port is dynamically
assigned when the service is created.</p>
</td>
</tr>
</tbody>
</table>
###PersistentVolumeEtcdStorageSpec { #hypershift.openshift.io/v1alpha1.PersistentVolumeEtcdStorageSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ManagedEtcdStorageSpec">ManagedEtcdStorageSpec</a>)
</p>
<p>
<p>PersistentVolumeEtcdStorageSpec is the configuration for PersistentVolume
etcd storage.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>storageClassName</code></br>
<em>
string
</em>
</td>
<td>
<em>(Optional)</em>
<p>StorageClassName is the StorageClass of the data volume for each etcd member.</p>
<p>See <a href="https://kubernetes.io/docs/concepts/storage/persistent-volumes#class-1">https://kubernetes.io/docs/concepts/storage/persistent-volumes#class-1</a>.</p>
</td>
</tr>
<tr>
<td>
<code>size</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#quantity-resource-api">
k8s.io/apimachinery/pkg/api/resource.Quantity
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>Size is the minimum size of the data volume for each etcd member.</p>
</td>
</tr>
</tbody>
</table>
###PlatformSpec { #hypershift.openshift.io/v1alpha1.PlatformSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>PlatformSpec specifies the underlying infrastructure provider for the cluster
and is used to configure platform specific behavior.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>type</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.PlatformType">
PlatformType
</a>
</em>
</td>
<td>
<p>Type is the type of infrastructure provider for the cluster.</p>
<p>
Value must be one of:
&#34;AWS&#34;, 
&#34;IBMCloud&#34;, 
&#34;None&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>aws</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AWSPlatformSpec">
AWSPlatformSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>AWS specifies configuration for clusters running on Amazon Web Services.</p>
</td>
</tr>
</tbody>
</table>
###PlatformType { #hypershift.openshift.io/v1alpha1.PlatformType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolPlatform">NodePoolPlatform</a>, 
<a href="#hypershift.openshift.io/v1alpha1.PlatformSpec">PlatformSpec</a>)
</p>
<p>
<p>PlatformType is a specific supported infrastructure provider.</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;AWS&#34;</p></td>
<td><p>AWSPlatform represents Amazon Web Services infrastructure.</p>
</td>
</tr><tr><td><p>&#34;IBMCloud&#34;</p></td>
<td><p>IBMCloudPlatform represents IBM Cloud infrastructure.</p>
</td>
</tr><tr><td><p>&#34;None&#34;</p></td>
<td><p>NonePlatform represents user supplied (e.g. bare metal) infrastructure.</p>
</td>
</tr></tbody>
</table>
###PublishingStrategyType { #hypershift.openshift.io/v1alpha1.PublishingStrategyType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ServicePublishingStrategy">ServicePublishingStrategy</a>)
</p>
<p>
<p>PublishingStrategyType defines publishing strategies for services.</p>
</p>
###Release { #hypershift.openshift.io/v1alpha1.Release }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ClusterVersionStatus">ClusterVersionStatus</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.NodePoolSpec">NodePoolSpec</a>)
</p>
<p>
<p>Release represents the metadata for an OCP release payload image.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>image</code></br>
<em>
string
</em>
</td>
<td>
<p>Image is the image pullspec of an OCP release payload image.</p>
</td>
</tr>
</tbody>
</table>
###ReplaceUpgrade { #hypershift.openshift.io/v1alpha1.ReplaceUpgrade }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolManagement">NodePoolManagement</a>)
</p>
<p>
<p>ReplaceUpgrade specifies upgrade behavior that replaces existing nodes
according to a given strategy.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>strategy</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.UpgradeStrategy">
UpgradeStrategy
</a>
</em>
</td>
<td>
<p>Strategy is the node replacement strategy for nodes in the pool.</p>
<p>
Value must be one of:
&#34;OnDelete&#34;, 
&#34;RollingUpdate&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>rollingUpdate</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.RollingUpdate">
RollingUpdate
</a>
</em>
</td>
<td>
<p>RollingUpdate specifies a rolling update strategy which upgrades nodes by
creating new nodes and deleting the old ones.</p>
</td>
</tr>
</tbody>
</table>
###RollingUpdate { #hypershift.openshift.io/v1alpha1.RollingUpdate }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ReplaceUpgrade">ReplaceUpgrade</a>)
</p>
<p>
<p>RollingUpdate specifies a rolling update strategy which upgrades nodes by
creating new nodes and deleting the old ones.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>maxUnavailable</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#intorstring-intstr-util">
k8s.io/apimachinery/pkg/util/intstr.IntOrString
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>MaxUnavailable is the maximum number of nodes that can be unavailable
during the update.</p>
<p>Value can be an absolute number (ex: 5) or a percentage of desired nodes
(ex: 10%).</p>
<p>Absolute number is calculated from percentage by rounding down.</p>
<p>This can not be 0 if MaxSurge is 0.</p>
<p>Defaults to 0.</p>
<p>Example: when this is set to 30%, old nodes can be deleted down to 70% of
desired nodes immediately when the rolling update starts. Once new nodes
are ready, more old nodes be deleted, followed by provisioning new nodes,
ensuring that the total number of nodes available at all times during the
update is at least 70% of desired nodes.</p>
</td>
</tr>
<tr>
<td>
<code>maxSurge</code></br>
<em>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.22/#intorstring-intstr-util">
k8s.io/apimachinery/pkg/util/intstr.IntOrString
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>MaxSurge is the maximum number of nodes that can be provisioned above the
desired number of nodes.</p>
<p>Value can be an absolute number (ex: 5) or a percentage of desired nodes
(ex: 10%).</p>
<p>Absolute number is calculated from percentage by rounding up.</p>
<p>This can not be 0 if MaxUnavailable is 0.</p>
<p>Defaults to 1.</p>
<p>Example: when this is set to 30%, new nodes can be provisioned immediately
when the rolling update starts, such that the total number of old and new
nodes do not exceed 130% of desired nodes. Once old nodes have been
deleted, new nodes can be provisioned, ensuring that total number of nodes
running at any time during the update is at most 130% of desired nodes.</p>
</td>
</tr>
</tbody>
</table>
###SecretEncryptionSpec { #hypershift.openshift.io/v1alpha1.SecretEncryptionSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>SecretEncryptionSpec contains metadata about the kubernetes secret encryption strategy being used for the
cluster when applicable.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>type</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.SecretEncryptionType">
SecretEncryptionType
</a>
</em>
</td>
<td>
<p>Type defines the type of kube secret encryption being used</p>
<p>
Value must be one of:
&#34;aescbc&#34;, 
&#34;kms&#34;
</p>
</td>
</tr>
<tr>
<td>
<code>kms</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.KMSSpec">
KMSSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>KMS defines metadata about the kms secret encryption strategy</p>
</td>
</tr>
<tr>
<td>
<code>aescbc</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.AESCBCSpec">
AESCBCSpec
</a>
</em>
</td>
<td>
<em>(Optional)</em>
<p>AESCBC defines metadata about the AESCBC secret encryption strategy</p>
</td>
</tr>
</tbody>
</table>
###SecretEncryptionType { #hypershift.openshift.io/v1alpha1.SecretEncryptionType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.SecretEncryptionSpec">SecretEncryptionSpec</a>)
</p>
<p>
<p>SecretEncryptionType defines the type of kube secret encryption being used.</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;aescbc&#34;</p></td>
<td><p>AESCBC uses AES-CBC with PKCS#7 padding to do secret encryption</p>
</td>
</tr><tr><td><p>&#34;kms&#34;</p></td>
<td><p>KMS integrates with a cloud provider&rsquo;s key management service to do secret encryption</p>
</td>
</tr></tbody>
</table>
###ServicePublishingStrategy { #hypershift.openshift.io/v1alpha1.ServicePublishingStrategy }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ServicePublishingStrategyMapping">ServicePublishingStrategyMapping</a>)
</p>
<p>
<p>ServicePublishingStrategy specfies how to publish a ServiceType.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>type</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.PublishingStrategyType">
PublishingStrategyType
</a>
</em>
</td>
<td>
<p>Type is the publishing strategy used for the service.</p>
</td>
</tr>
<tr>
<td>
<code>nodePort</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.NodePortPublishingStrategy">
NodePortPublishingStrategy
</a>
</em>
</td>
<td>
<p>NodePort configures exposing a service using a NodePort.</p>
</td>
</tr>
</tbody>
</table>
###ServicePublishingStrategyMapping { #hypershift.openshift.io/v1alpha1.ServicePublishingStrategyMapping }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.HostedClusterSpec">HostedClusterSpec</a>, 
<a href="#hypershift.openshift.io/v1alpha1.HostedControlPlaneSpec">HostedControlPlaneSpec</a>)
</p>
<p>
<p>ServicePublishingStrategyMapping specifies how individual control plane
services are published from the hosting cluster of a control plane.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>service</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ServiceType">
ServiceType
</a>
</em>
</td>
<td>
<p>Service identifies the type of service being published.</p>
</td>
</tr>
<tr>
<td>
<code>servicePublishingStrategy</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.ServicePublishingStrategy">
ServicePublishingStrategy
</a>
</em>
</td>
<td>
<p>ServicePublishingStrategy specifies how to publish Service.</p>
</td>
</tr>
</tbody>
</table>
###ServiceType { #hypershift.openshift.io/v1alpha1.ServiceType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ServicePublishingStrategyMapping">ServicePublishingStrategyMapping</a>)
</p>
<p>
<p>ServiceType defines what control plane services can be exposed from the
management control plane.</p>
</p>
###UnmanagedEtcdSpec { #hypershift.openshift.io/v1alpha1.UnmanagedEtcdSpec }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.EtcdSpec">EtcdSpec</a>)
</p>
<p>
<p>UnmanagedEtcdSpec specifies configuration which enables the control plane to
integrate with an eternally managed etcd cluster.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>endpoint</code></br>
<em>
string
</em>
</td>
<td>
<p>Endpoint is the full etcd cluster client endpoint URL. For example:</p>
<pre><code>https://etcd-client:2379
</code></pre>
<p>If the URL uses an HTTPS scheme, the TLS field is required.</p>
</td>
</tr>
<tr>
<td>
<code>tls</code></br>
<em>
<a href="#hypershift.openshift.io/v1alpha1.EtcdTLSConfig">
EtcdTLSConfig
</a>
</em>
</td>
<td>
<p>TLS specifies TLS configuration for HTTPS etcd client endpoints.</p>
</td>
</tr>
</tbody>
</table>
###UpgradeStrategy { #hypershift.openshift.io/v1alpha1.UpgradeStrategy }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.ReplaceUpgrade">ReplaceUpgrade</a>)
</p>
<p>
<p>UpgradeStrategy is a specific strategy for upgrading nodes in a NodePool.</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;OnDelete&#34;</p></td>
<td><p>UpgradeStrategyOnDelete replaces old nodes when the deletion of the
associated node instances are completed.</p>
</td>
</tr><tr><td><p>&#34;RollingUpdate&#34;</p></td>
<td><p>UpgradeStrategyRollingUpdate means use a rolling update for nodes.</p>
</td>
</tr></tbody>
</table>
###UpgradeType { #hypershift.openshift.io/v1alpha1.UpgradeType }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.NodePoolManagement">NodePoolManagement</a>)
</p>
<p>
<p>UpgradeType is a type of high-level upgrade behavior nodes in a NodePool.</p>
</p>
<table>
<thead>
<tr>
<th>Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr><td><p>&#34;InPlace&#34;</p></td>
<td><p>UpgradeTypeInPlace is a strategy which replaces nodes in-place with no
additional node capacity requirements.</p>
</td>
</tr><tr><td><p>&#34;Replace&#34;</p></td>
<td><p>UpgradeTypeReplace is a strategy which replaces nodes using surge node
capacity.</p>
</td>
</tr></tbody>
</table>
###Volume { #hypershift.openshift.io/v1alpha1.Volume }
<p>
(<em>Appears on:</em>
<a href="#hypershift.openshift.io/v1alpha1.AWSNodePoolPlatform">AWSNodePoolPlatform</a>)
</p>
<p>
<p>Volume specifies the configuration options for node instance storage devices.</p>
</p>
<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>
<code>size</code></br>
<em>
int64
</em>
</td>
<td>
<p>Size specifies size (in Gi) of the storage device.</p>
<p>Must be greater than the image snapshot size or 8 (whichever is greater).</p>
</td>
</tr>
<tr>
<td>
<code>type</code></br>
<em>
string
</em>
</td>
<td>
<p>Type is the type of the volume.</p>
</td>
</tr>
<tr>
<td>
<code>iops</code></br>
<em>
int64
</em>
</td>
<td>
<em>(Optional)</em>
<p>IOPS is the number of IOPS requested for the disk. This is only valid
for type io1.</p>
</td>
</tr>
</tbody>
</table>
<hr/>