# ADR-002 — Backend Framework Selection

**Date:** 03/04/2026  
**Status:** Accepted

## Decision
.NET 8 Web API

## Reason
- Comfortable with C# and .NET ecosystem
- EF Core 8 code-first migrations
- Built-in JWT support via System.IdentityModel
- All 9 microservices will use same framework
- Single CI/CD pipeline pattern across all services