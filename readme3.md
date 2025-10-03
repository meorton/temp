# Cloud Artifact Registry / CDN Options for Global Deployment

## Executive Summary

This document provides verified information about cloud provider options for hosting container images and artifacts across your global locations: Kuwait, Saudi Arabia, Argentina, Colombia, and various US states.

---

## Your Location Distribution

Based on your provided locations, here's the breakdown:

| Region | Locations | Count |
|--------|-----------|-------|
| **Middle East** | Kuwait, Saudi Arabia | 7 sites |
| **South America** | Argentina, Colombia | 18 sites |
| **United States** | WTX, STX, ETX, ND, NE, WSTRN | 95+ sites |
| **Other** | PNG (Papua New Guinea), Breen Yard | 2 sites |

**Total Sites**: ~122 locations pulling container images

---

## Provider Comparison Table

| Provider | Best Regions for Your Locations | Pricing Model | Regional Control | Best For |
|----------|--------------------------------|---------------|------------------|----------|
| **Azure Container Registry** | ✅ Excellent coverage | Pay-as-you-go | ✅ Full control | Enterprise deployments with geo-replication needs |
| **GitHub Packages** | ⚠️ Limited (global CDN only) | Free for public, tiered for private | ❌ No regional selection | Open source projects, small teams |
| **Nexus Repository** | ✅ You control all locations | Self-hosted + infrastructure costs | ✅ Complete control | Maximum flexibility, air-gapped environments |

---

## Option 1: Azure Container Registry (Recommended)

### Available Regions for Your Locations

| Your Locations | Nearest Azure Region | Latency Expectation |
|----------------|---------------------|---------------------|
| Kuwait, Saudi Arabia | **UAE Central** (Abu Dhabi)<br>**UAE North** (Dubai)<br>**Qatar Central**<br>**Saudi Arabia East** (Dammam - under construction) | Low (< 50ms) |
| Argentina, Colombia | **Brazil South** (São Paulo)<br>**Brazil Southeast** | Medium (50-100ms from Argentina)<br>Higher from Colombia |
| US Sites (TX, ND, NE, etc.) | **East US** (Virginia)<br>**Central US** (Iowa)<br>**West US** (California)<br>**South Central US** (Texas) | Very Low (< 20ms) |

### Pricing (USD - Official Azure Pricing)

#### Registry Tiers

| Tier | Daily Cost | Monthly Cost* | Included Storage | Geo-Replication | Best For |
|------|-----------|--------------|------------------|-----------------|----------|
| **Basic** | $0.167/day | ~$5.00/month | 10 GB | ❌ No | Development/Testing |
| **Standard** | $0.667/day | ~$20.00/month | 100 GB | ❌ No | Small production workloads |
| **Premium** | $1.667/day | ~$50.00/month | 500 GB | ✅ Yes ($1.667/day per region) | **Recommended for your use case** |

*Monthly cost = Daily cost × 30 days

#### Additional Costs

| Item | Cost | Notes |
|------|------|-------|
| **Extra Storage** | $0.00334/day per GB | ~$0.10/month per GB |
| **Build Tasks** | $0.0001/second | Only if using Azure Container Registry Tasks |
| **Data Transfer OUT** | See table below | First 100 GB/month FREE |

#### Data Transfer (Egress) Pricing

| Source Region | First 100 GB/month | Next 10 TB/month | Next 40 TB/month | Next 100 TB/month |
|---------------|-------------------|------------------|------------------|-------------------|
| **North America, Europe** → Any | FREE | $0.087/GB | $0.083/GB | $0.07/GB |
| **Middle East, Asia** → Any | FREE | $0.12/GB | $0.085/GB | $0.082/GB |
| **South America** → Any | FREE | $0.181/GB | $0.175/GB | $0.17/GB |

**Note**: Data transfer IN is always FREE

#### Geo-Replication Cost Example

For your global deployment with Premium tier:
- **Base Registry**: $50/month (UAE Central)
- **Replica in Brazil South**: +$50/month
- **Replica in US Central**: +$50/month
- **Total**: $150/month + storage + egress

### Key Features
- ✅ Low latency for all your regions
- ✅ Geo-replication keeps images close to users
- ✅ Enterprise security and compliance
- ✅ Integration with Azure services
- ✅ Automatic image scanning (with Defender)

---

## Option 2: GitHub Packages

### Regional Availability

| Feature | Details |
|---------|---------|
| **CDN Coverage** | Global edge network (exact PoPs not disclosed) |
| **Data Residency** | Limited to: US, EU, Australia only |
| **Regional Selection** | ❌ Not available - GitHub controls routing |

⚠️ **Important Limitation**: You cannot choose to store data in Middle East or South America regions specifically.

### Pricing (USD - Official GitHub Pricing)

#### Free Tier (All Plans)
- **Public Packages**: Unlimited storage and bandwidth (FREE forever)
- **Container Registry**: Currently FREE (GitHub will provide 1-month notice before any changes)

#### Private Packages Pricing

| Plan | Storage Included | Data Transfer/Month | Monthly Cost |
|------|------------------|---------------------|--------------|
| **GitHub Free** | 500 MB | 1 GB | $0 |
| **GitHub Pro** | 2 GB | 10 GB | $4/user/month |
| **GitHub Team** | 2 GB | 10 GB | $4/user/month |
| **GitHub Enterprise Cloud** | 50 GB | 100 GB | $21/user/month |

#### Overage Pricing
- **Storage**: Not publicly listed - contact GitHub
- **Data Transfer**: Not publicly listed - contact GitHub
- Usage blocked if no payment method on file

### Key Features
- ✅ Free for public packages
- ✅ Simple integration with GitHub Actions
- ✅ No infrastructure management
- ❌ Limited regional control
- ❌ Not ideal for Middle East/South America latency optimization

---

## Option 3: Nexus Repository (Sonatype)

### Deployment Model

| Aspect | Details |
|--------|---------|
| **Hosting** | Self-hosted (you manage infrastructure) |
| **Regional Proxies** | Deploy anywhere you want |
| **Flexibility** | Complete control over all locations |

### Architecture Options

You can deploy:
1. **Central Nexus** in one region (e.g., US)
2. **Regional Proxy Caches** in:
   - UAE (for Kuwait/Saudi Arabia)
   - Brazil (for Argentina/Colombia)
   - Multiple US regions

### Pricing

| Edition | Cost | Features |
|---------|------|----------|
| **Community (OSS)** | FREE | Basic repository management |
| **Professional** | Contact Sales | High availability, staging, LDAP, etc. |

**Additional Costs You'll Need**:
- Server infrastructure (VMs, Kubernetes, etc.)
- Storage (local or cloud object storage like S3)
- Network bandwidth
- Maintenance and operations staff

### Estimated Infrastructure Costs (Example)

For a global deployment:

| Component | Estimated Monthly Cost |
|-----------|----------------------|
| Central Nexus (AWS/Azure VM) | $200-500 |
| Regional Proxies (3 locations) | $150-300 each = $450-900 |
| Storage (S3/Azure Blob) | $50-200 (depends on volume) |
| Data Transfer | $100-500 (depends on usage) |
| **Total Infrastructure** | **$800-2,100/month** |
| Nexus Pro License | Contact Sonatype Sales |

### Key Features
- ✅ Maximum flexibility and control
- ✅ Can work in air-gapped environments
- ✅ Support for all package formats
- ✅ On-premises or cloud deployment
- ❌ Requires infrastructure management
- ❌ Higher operational overhead

---

## Recommendation for Your Use Case

### Primary Recommendation: **Azure Container Registry Premium with Geo-Replication**

**Why?**
1. **Best regional coverage** for your 122 sites across Middle East, South America, and US
2. **Predictable costs** with clear pricing structure
3. **Low latency** through geo-replication to UAE, Brazil, and US regions
4. **Enterprise-grade** security, compliance, and SLA
5. **Managed service** - no infrastructure overhead

**Estimated Monthly Cost**:
- Base Premium Registry: $50
- 2 Geo-replicas (Brazil, US): $100
- Storage (assuming 1TB): $100
- Data Transfer (assuming 5TB/month): $435-905 (varies by region)
- **Total**: ~$685-1,155/month

### Alternative: **GitHub Packages** (If Applicable)

**Good for**:
- Public/open-source projects (FREE)
- Small teams with light usage
- Projects already using GitHub heavily

**Not ideal for**:
- Latency-sensitive workloads in Middle East/South America
- Large-scale enterprise deployments
- Compliance requirements for data residency

### Alternative: **Nexus Repository** (For Special Cases)

**Good for**:
- Air-gapped or highly regulated environments
- Need to support multiple package formats beyond containers
- Want complete control over infrastructure
- Already have DevOps team to manage it

**Not ideal for**:
- Teams wanting managed services
- Organizations without infrastructure expertise
- Cost-sensitive projects (higher total cost of ownership)

---

## Next Steps

1. **Estimate your actual usage**:
   - How many GB of images will you store?
   - How much data transfer per month? (images pulled × size × frequency)
   - How many regions need low latency?

2. **Use Azure Pricing Calculator**: https://azure.microsoft.com/en-us/pricing/calculator/

3. **Consider a pilot**:
   - Start with Azure Container Registry Premium in one region
   - Test latency from your key locations
   - Add geo-replicas as needed

4. **For GitHub Packages**: Check if your packages can be public (FREE)

5. **For Nexus**: Contact Sonatype sales for Professional edition pricing

---

## Additional Resources

- [Azure Container Registry Documentation](https://docs.microsoft.com/en-us/azure/container-registry/)
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
- [GitHub Packages Documentation](https://docs.github.com/en/packages)
- [Nexus Repository Documentation](https://help.sonatype.com/en/sonatype-nexus-repository.html)

---

**Document Version**: 1.0  
**Last Updated**: January 2025  
**Sources**: Official Azure, GitHub, and Sonatype documentation
