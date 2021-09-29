# SNARK as a Service

Computing SNARK proofs can be extremely computationally expensive, often well outside the capabilities of client devices.
SNARK as a Service leverages [rapidsnark](https://github.com/iden3/rapidsnark) executing in a [Confidential VM](https://cloud.google.com/confidential-computing)
in order to allow clients to offload their proof generation to cloud computing resources, opening the possibility for
very large SNARK circuits to be used in trust-limited circumstances.

Conceptual Design:
* Custom image [compiled with AMD SEV et al](https://cloud.google.com/compute/confidential-vm/docs/how-to-byoi)
* Image includes absolute minimum environment to run an HTTPS service wrapping rapidsnark
* VM boot options:
    * [CSEK](https://cloud.google.com/compute/docs/disks/customer-supplied-encryption#rsa-encryption) for any storage
    * [Shielded VM](https://cloud.google.com/security/shielded-cloud/shielded-vm)
    * Ensure that there are no Google management services (e.g. accounts daemon)
    * Disable automatic restart
* 

Nice to Haves:
* GCP-level [Tenant Isolation](https://cloud.google.com/service-infrastructure/docs/manage-tenancy-units)
* [Sole Tenant Nodes](https://cloud.google.com/compute/docs/nodes/sole-tenant-nodes)
* Statically estimate the compute cost of executing a particular circuit

Trust Requirements:
* 
