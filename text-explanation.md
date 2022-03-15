DevOps Challenge Explanation
============================


Thought Process
---------------

For the most part I was aiming for a balance between a 'minimal viable product'
and sufficient polish to display my abilities within the time I had. The 
repository is not fully production ready but should be sufficient to meet the
requirements and give you an idea of what I can do. I've left some issues open
in the repository to show at least **some** of the things that would still need to
be fixed before this was fully usable.

Whatever I may be working on, I always have a few considerations in mind: 
- Make it modular and resuable
- Make it consistent and manageable (maintainable/sustainable)
- Make it secure
- Keep it simple and understandable

Given the parameters of the challenge, I kept to writing everything from 
scratch rather than using existing roles. Many times this is preferred 
anyway as I've found publicly available roles to often have
significant shortcomings, not only in and of themselves, but using a bunch of
public roles often results in massive inconsistencies that make everything 
less manageable in the future.


Technology Choices
------------------

- Ansible: I've used only Ansible because I'm more familiar with it than Terraform 
  or Chef, and it's perfectly capable of doing everything needed, therefore it 
  made the most sense given the limited timeframe I had to complete everything.

- Debian VMs: I've used Debian VMs mainly for the same reason. My homelab is 
  mostly Debian, though I have plenty of familiarity with many other 
  distributions. Other than the proxmox_vm role (because Proxmox only 
  supports running in Debian), the rest should require minimal changes to 
  work with other distributions.

- Proxmox: I've written this to deploy against Proxmox VE, once again because
  that's what I use at home. Given a role for any other hypervisor or cloud, 
  it will be very simple to have this app deploy anywhere.


Architecture
------------

**Deployment**

The deployment playbook will deploy a single haproxy server that will forward
requests to one or more back-end application servers. The sample application
will return the name of the application server that served the request. 

The haproxy configuration as written uses cookies to keep connections
persistent to the same back-end. To test returning different app server names,
you can block cookies for the URL and refresh your browser.

NOTE: I have not included my encrypted vault files/password that would be
required for this to run in another environment.


**Decommission**

A second playbook is provided to decommission and destroy all of the VMs
associated with the application.



Roles
-----

I wrote three roles for this exercise, but kept them very basic and minimal.  
They need a fair amount of work before I'd actually consider them properly
usable. 

- proxmox_vm: Uses the community.general.proxmox_kvm module to clone VMs from
  a template on deployment, and to destroy the VMs on decommission. What I have
  here is very basic. Ideally I'd eventually end up with a role that reusably 
  supported much more of the functionality available via the proxmox_kvm module.

- haproxy: Uses basic builtin modules to install the package, build a config
  file from a template and managing the service. This again is very basic
  in its current form. 

- challenge1_app: Because I don't come from a development background, I chose
  to deploy a very, very basic back-end python app using flask and gunicorn.
  The role installs the needed packages and because the app itself is so small
  it deploys it from a template that will return the name of whichever app server
  it is running on.

Issues
------

I've left in place issues for **some** (though certainly not all) of the issues
and shortcomings I'm aware of. There's a lot more polish that I would absolutely 
complete before I'd call it ready for production but I'm hoping that level of
polish isn't necessary to give you an idea of my abilities and where I still have
things to learn.


Challenge Requirements
----------------------

Fully automated sample application environment using Ansible, Terraform, 
Chef and/or pure code to provision, manage and eventually destroy a 
minimum two-tier sample application of the applicant’s choice.  
The front-end URL/endpoint should be returned as an output and accessible 
once execution is complete.

- Solution submission must be shared via git repository link
- CentOS, Redhat Enterprise Linux (RHEL), Debian or Ubuntu should be used as 
  the base operating system
- The solution may be containerized, however, this not required
- The solution must be designed in a reusable, production oriented manner
- Documentation (readme, etc) should be included for the submitted solution
- Original code by the applicant with all references, licenses or any forks 
  properly acknowledged and used only where it is necessary or additional 
 benefits are provided
- The applicant does NOT need to build the application components/artifacts
- Text explanation on the applicant’s approach including a brief overview of 
  the architecture and thought process towards the desired challenge outcome
