[Do you air-gap environments so that no single service account can cross environment boundaries?]
[Yes. Teams get their own landing zone (network spoke and cloud project/subscription/account i.e. their own corner of the cloud). Landing zones have baseline settings through policies (e.g. public IPs are not allowed and must be approved. Often a Slack thread is enough).]
[Do you allow developers to deploy to dev/sandbox/test environments?]
[Yes. They own all their environments. They also get access to a sandbox environment which is completely air-gapped from the organization and has policies that restrict expensive resources and automations that nuke it org-wide every now and then.]
[Can developers administer service accounts / iam permissions on dev environments?]
[Yes. They get IAM ownership on their own landing zone. Their responsibility. However, governance team looks over the initial phases, e.g. prod environment does not exist before someone checks that their dev/staging look reasonable.]
[How about global resources like buckets?]
[Shared resources are owned by the cloud / governance team. So no. Unless it's their own resource of course, like in a shared environment (for example, artifact registries for their software artifacts that are promoted through environments).]
[How do you provision access for their project pipelines to do what they need to without risking the pipeline escalating its own privileges to break other infrastructure?]
[Pipeline jobs run in containers. Containers run in ephemeral hosts (Cloud Run / Azure Container Apps / Elastic Container Service or just VMs). Users can only access the resources their service accounts / credentials can, so they are limited to their own environment. Bootstrapping the landing zone and its accompanying services like CICD IAM, repository and pipeline templates are done through a Terraform module.]
[If Service A needs Resource Alpha running as Service Account Alphonso, how do you let the their pipeline create A, Alpha, and Alphonso without permitting read/mutation/deletion of service B, resource Beta, and account Brit? Is that even a real issue?]
[Again, they own their own infrastructure and automation and are limited to their own environment. Assuming A and B are owned by different teams, it's impossible. Assuming they are owned by the same team, their credentials have the required access to do wide changes.]
[What about Shared Resource Gamma? Or do you take away rights to deploy any infrastructure and only allow pipelines to revision deployed code?]
[Assuming this is an organization-wide shared resource and not their own shared resource, they request it or the most tech-savvy personnel push a PR and sends the cloud team a link to review and merge.]
[Are these just squishy details and ideas that don't really matter so long as there's a point person who's accountable for policy?]
[No they are very important details for a robust scalable SDLC. Policy-side is generally owned by a cloud governance team. Smaller decisions are made internally in that team (participating stakeholders of course). Bigger decisions go through architecture review boards and then trickle down to the governance team. Technology choices and organization-wide changes are discussed in the CCoE (Cloud Center of Excellence) team meetings, which consist of business, architecture and engineers.]
[Hope that helps.]
[What do you think air-gapped means?]
[I doubt that they meant TEMPEST controls but the principles of separation between different logical and physical computer networks are an important distinction. There are some really interesting reading materials about how to jump across air gaps but I'm expecting that five nines of the IT industry have never had to think about that.]
[Physically separated (disconnected) i.e. isolated. What do you think I  mean with air-gapped in the context of this post?]
[Yep that is exactly it.]
[You use the term ‘landing zone’ a little bit strangely here for what I’m used to but I think I agree with you completely and do the same.]
[However to clarify, landing zone we mean in the aws sense where we control the org/platform/rollout of account and some guardrails and deliver ‘fully functional aws accounts with preconfigured networking and guardrails’.]
[Devs are then 100% responsible for that set of account and everything in it, what we term ‘the workload’ which is the security and billing boundary of everything they do there.]
[Is that what you mean?]
[Oversight is provided by the platform with built in stuff like security hub and the aws services that integrate the spoke controls back to a central account.]
[Doing that allows everything to become an uncontrollable shitshow everywhere, really fast just like every enterprise. VELOCITY (half joking about this bit).]
[Thank you so much for the super detailed response, this is really helpful. Obviously nothing is law and needs to be informed by cloud governance / [business + architecture + eng + infosec] but I'm realizing my task is now is to get the all of the correct people in the room on a regular basis to talk about how we scale SDLC with compliance tasks instead of trying to figure it out between the devops lead and I as we go.]
[This is a real challenge though at my company since we don't have an architect or anyone even remotely EA informed, or infosec informed for that matter. My org operates like a startup being incubated in a segregated little corner of the company and unfortunately a lot of interaction with the rest of the business becomes a political quagmire very quickly. If you have any tips on how to build a CCoE coalition in absence of proper resourcing as a developer (with non-negligible leadership clout, but still young), I promise to pay the wisdom forward as best I can.]
[Sadly I don't have tips to offer for you other than that the transformation must be driven by the business or it will never succeed. It's a major undertaking that requires buy-in across the company. Often these things are done during cloud transformation journeys with external help.]
# Reddit Comment Thread


**NUTTA_BUSTAH**
> Do you air-gap environments so that no single service account can cross environment boundaries?


> Do you allow developers to deploy to dev/sandbox/test environments?


> Can developers administer service accounts / iam permissions on dev environments?


> How about global resources like buckets?


> How do you provision access for their project pipelines to do what they need to without risking the pipeline escalating its own privileges to break other infrastructure?


> If Service A needs Resource Alpha running as Service Account Alphonso, how do you let the their pipeline create A, Alpha, and Alphonso without permitting read/mutation/deletion of service B, resource Beta, and account Brit? Is that even a real issue?


> What about Shared Resource Gamma? Or do you take away rights to deploy any infrastructure and only allow pipelines to revision deployed code?


> Are these just squishy details and ideas that don't really matter so long as there's a point person who's accountable for policy?


Do you air-gap environments so that no single service account can cross environment boundaries?
Yes. Teams get their own landing zone (network spoke and cloud project/subscription/account i.e. their own corner of the cloud). Landing zones have baseline settings through policies (e.g. public IPs are not allowed and must be approved. Often a Slack thread is enough).
Do you allow developers to deploy to dev/sandbox/test environments?
Yes. They own all their environments. They also get access to a sandbox environment which is completely air-gapped from the organization and has policies that restrict expensive resources and automations that nuke it org-wide every now and then.
Can developers administer service accounts / iam permissions on dev environments?
Yes. They get IAM ownership on their own landing zone. Their responsibility. However, governance team looks over the initial phases, e.g. prod environment does not exist before someone checks that their dev/staging look reasonable.
How about global resources like buckets?
Shared resources are owned by the cloud / governance team. So no. Unless it's their own resource of course, like in a shared environment (for example, artifact registries for their software artifacts that are promoted through environments).
How do you provision access for their project pipelines to do what they need to without risking the pipeline escalating its own privileges to break other infrastructure?
Pipeline jobs run in containers. Containers run in ephemeral hosts (Cloud Run / Azure Container Apps / Elastic Container Service or just VMs). Users can only access the resources their service accounts / credentials can, so they are limited to their own environment. Bootstrapping the landing zone and its accompanying services like CICD IAM, repository and pipeline templates are done through a Terraform module.
If Service A needs Resource Alpha running as Service Account Alphonso, how do you let the their pipeline create A, Alpha, and Alphonso without permitting read/mutation/deletion of service B, resource Beta, and account Brit? Is that even a real issue?
Again, they own their own infrastructure and automation and are limited to their own environment. Assuming A and B are owned by different teams, it's impossible. Assuming they are owned by the same team, their credentials have the required access to do wide changes.
What about Shared Resource Gamma? Or do you take away rights to deploy any infrastructure and only allow pipelines to revision deployed code?
Assuming this is an organization-wide shared resource and not their own shared resource, they request it or the most tech-savvy personnel push a PR and sends the cloud team a link to review and merge.
Are these just squishy details and ideas that don't really matter so long as there's a point person who's accountable for policy?
No they are very important details for a robust scalable SDLC. Policy-side is generally owned by a cloud governance team. Smaller decisions are made internally in that team (participating stakeholders of course). Bigger decisions go through architecture review boards and then trickle down to the governance team. Technology choices and organization-wide changes are discussed in the CCoE (Cloud Center of Excellence) team meetings, which consist of business, architecture and engineers.
Hope that helps.
Hope that helps.

---

  **DensePineapple** (reply to NUTTA_BUSTAH)
  > What do you think air-gapped means?

    **m4nf47** (reply to DensePineapple)
    I doubt that they meant TEMPEST controls but the principles of separation between different logical and physical computer networks are an important distinction. There are some really interesting reading materials about how to jump across air gaps but I'm expecting that five nines of the IT industry have never had to think about that.

    **NUTTA_BUSTAH** (reply to DensePineapple)
    Physically separated (disconnected) i.e. isolated. What do you think I  mean with air-gapped in the context of this post?

  **dogfish182** (reply to NUTTA_BUSTAH)
  You use the term ‘landing zone’ a little bit strangely here for what I’m used to but I think I agree with you completely and do the same.

  However to clarify, landing zone we mean in the aws sense where we control the org/platform/rollout of account and some guardrails and deliver ‘fully functional aws accounts with preconfigured networking and guardrails’.

  Devs are then 100% responsible for that set of account and everything in it, what we term ‘the workload’ which is the security and billing boundary of everything they do there.

  Is that what you mean?

  Oversight is provided by the platform with built in stuff like security hub and the aws services that integrate the spoke controls back to a central account.

  Doing that allows everything to become an uncontrollable shitshow everywhere, really fast just like every enterprise. VELOCITY (half joking about this bit).

    **NUTTA_BUSTAH** (reply to dogfish182)
    Yep that is exactly it.

  **dongus_nibbler** (reply to NUTTA_BUSTAH)
  Thank you so much for the super detailed response, this is really helpful. Obviously nothing is law and needs to be informed by cloud governance / [business + architecture + eng + infosec] but I'm realizing my task is now is to get the all of the correct people in the room on a regular basis to talk about how we scale SDLC with compliance tasks instead of trying to figure it out between the devops lead and I as we go.

  This is a real challenge though at my company since we don't have an architect or anyone even remotely EA informed, or infosec informed for that matter. My org operates like a startup being incubated in a segregated little corner of the company and unfortunately a lot of interaction with the rest of the business becomes a political quagmire very quickly. If you have any tips on how to build a CCoE coalition in absence of proper resourcing as a developer (with non-negligible leadership clout, but still young), I promise to pay the wisdom forward as best I can.

    **NUTTA_BUSTAH** (reply to dongus_nibbler)
    Sadly I don't have tips to offer for you other than that the transformation must be driven by the business or it will never succeed. It's a major undertaking that requires buy-in across the company. Often these things are done during cloud transformation journeys with external help.

---

(End of thread. All comments and replies are included. Indentation and author labels show reply structure.)
