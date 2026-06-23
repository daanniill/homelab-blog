# Intro

Hello! This blog marks the beginning of what will likely be a long and challenging journey into the world of homelabbing. I decided to document the process so that the lessons I learn along the way can be recorded, revisited, and hopefully useful to both my future self and anyone else who happens to find this blog.

When I first started exploring homelabbing, one of the most interesting—and slightly intimidating—things I noticed was that there is no single, clearly defined path to follow. There is no exact list of projects you are supposed to complete or skills you are guaranteed to learn. As someone who usually prefers structure and clear direction, I initially found that uncertainty a little unsettling.

At the same time, that freedom is what makes homelabbing so interesting. You can experiment, build almost anything you can imagine, make mistakes, and learn through the process of creating.

I hope this blog can serve as a kind of treasure map for anyone who discovers it in the future. Maybe someone will retrace my steps, or perhaps they will take a few detours and find their own version of the treasure (whether this treasure may be a swe or cyber job).

Most of all, I hope this blog allows me to look back and see how much I have improved. I want it to keep me motivated, encourage me to reflect on my experiences, and document everything I encounter along the way.


# Building My First Homelab

My homelab started with two inexpensive enterprise servers I found on Facebook Marketplace, a switch I got off of newegg, and some aliexpress ddr3 ram:

- Dell PowerEdge R210 ($20)
- Dell PowerEdge R220 ($50)
- Netgear GS305E managed switch ($20)
- 24 GB DDR3 of RAM from AliExpress ($50)

![current_setup](/Users/daniil/Desktop/personal_projects/homelab-blog/images/cur_setup.jpeg)


I initially wanted to just get the dell r220, but the r210 that I saw on marketplace provided some cool donor parts such as rails and bezels that I just couldn't pass up on. The r220 initially came with 16 GB of ram and the r210 came with 12 GB, so I decided to invest in three 8 GB sticks from AliExpress, as I knew that sufficient memory would be something that would be vey useful for some of the initial plans that I had for my homelab, such as web hosting and game servers. 

![r210](/Users/daniil/Desktop/personal_projects/homelab-blog/images/r210.jpg)
![r220](/Users/daniil/Desktop/personal_projects/homelab-blog/images/r220.jpg)

I also wanted to create a cluster, so having at least two machines would allow me to learn how to balance multiple nodes in a network and also allow for redundancy in my network.

## My first significant issues

The first significant issue I ran into was storage. The R210 did not come with any drive cages, which meant I had no proper way to mount the SSDs and hard drives I planned to use. Looking online, r210 drive cages were as rare as antimatter, and the ones that I was able to find on ebay were all $30+, a price I was not willing to pay especially considering the whole server cost me $20. So rather than buying the drive cages, I found some designs online and contracted my cousing to 3D print a custom mount that could hold 3 standard 2.5-inch SSDs. 

![ssd_tray](/Users/daniil/Desktop/personal_projects/homelab-blog/images/ssd_tray_r210.jpeg)

My power-management situation was also nearly nonexistent. At first, both servers, the switch, and the surrounding equipment were connected through a messy collection of cables and outlets. It quickly became clear that this was neither organized nor particularly safe. I redid the wiring and purchased a surge protector for around $20 so that the equipment would have at least some basic protection and the setup would be easier to manage.

Another unexpected obstacle was that I did not have a convenient way to interact directly with the servers during installation. Since both machines use VGA output, I picked up a cheap monitor and VGA cable from Goodwill for about $12. It was not glamorous, but it gave me everything I needed to access the BIOS, configure the machines, and begin installing Proxmox.

Getting storage was a whole new adventure itself. Instead of buying all-new drives, I searched around the house for unused hardware and managed to find an 825 GB SATA drive, a 1 TB SATA drive, and a 128 GB SSD. I decided to use the 128 GB SSD as the Proxmox boot drive for the R210, while utilizing the larger drives for virtual machines, containers, backups, and other services on my r220. I also had OEM drive cages in the r220 which was a plus.

Although none of these problems were especially complicated on their own, they showed me how quickly the cost and complexity of a homelab can grow beyond the original servers. Rails, drive mounts, cables, power protection, monitors, and storage are easy to overlook when planning a setup. At the same time, finding inexpensive or improvised solutions became part of the fun.

## Total Cost So Far

By the time I had both servers powered, connected, and ready for Proxmox, my total investment came to approximately $172.

Hardware and Equipment

- Dell PowerEdge R210 — $20
- Dell PowerEdge R220 — $50
- Netgear GS305E managed switch — $20
- 24 GB of DDR3 RAM from AliExpress — $50
- Surge protectors and power-management supplies — $20
- Monitor and VGA cable from Goodwill — $12
- Custom 3D-printed SSD caddy for the R210 — $0
- 128 GB SSD for the R210 Proxmox boot drive — $0
- 825 GB SATA drive — $0
- 1 TB SATA drive — $0
- Rails and bezels included with the R210 — $0

Total: $172

## Why I Built It

My main goal was to create an environment where I could experiment with virtualization, networking, linux , containers, and self-hosted software without depending entirely on cloud infrastructure.

I spend a lot of time learning software development, but I wanted to better understand what happens after an application is written. I wanted experience deploying applications, managing servers, configuring networks, monitoring services, and troubleshooting the infrastructure that keeps everything running.

## Installing Proxmox

Once the hardware was assembled and the storage situation was mostly resolved, I installed Proxmox VE on both servers with the help of the Proxmox tutorial series by Learn Linux TV on YouTube. [tutorial](https://www.youtube.com/playlist?list=PLT98CRl2KxKHnlbYhtABg6cF50bYa8Ulo)

The R220 became my primary virtualization machine because it had more memory and better storage options. I planned to use it for larger virtual machines, containers, game servers, and hosted applications. The R210 would handle lighter workloads, infrastructure experiments, and services that could benefit from running on a separate physical machine.

After completing the installations, I updated both systems:

```bash
  apt update
  apt full-upgrade
```

At this stage, I configured the machines as separate Proxmox nodes. My next goal is to connect them more closely and experiment with clustering, shared management, backups, and redundancy.

Installing Proxmox was the first point where the collection of used hardware began to feel like an actual homelab. Instead of simply owning two old servers, I now had a platform on which I could begin building and managing real services.

## What I Plan to Build

There are several projects I would like to explore as the homelab develops:

- Docker containers for self-hosted applications
- Web hosting for personal projects
- Multiplayer game servers
- Network and system monitoring
- Local development and testing environments
- Automated backups
- Virtual networks and firewall configurations
- A small Kubernetes cluster
- Local GitHub Actions runners
- Experiments with high availability and redundancy

I do not expect to build everything immediately. Part of the purpose of this blog is to document each project individually, including the mistakes, configuration problems, and lessons that come with it.

## What I Learned

The biggest lesson from this first stage was that inexpensive hardware is not always inexpensive to operate or complete. A server may only cost $20 or $50, but it may still need additional memory, storage, drive mounts, cables, networking equipment, and power protection before it becomes useful.

I also learned that improvisation is a major part of homelabbing. The missing R210 drive cage could have stopped the project, but a 3D-printed mount provided a practical alternative. 

None of these solutions were especially elegant, but they worked and finding those solutions was part of the experience.

At this point, the homelab is still in its earliest stage. I have the hardware, networking equipment, storage, and virtualization platform needed to begin experimenting. The next step is to start building services, breaking configurations, fixing them, and documenting what I learn along the way.

