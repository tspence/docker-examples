# As of August 2023, I believe this is the current version of SQL Server available for use
FROM mcr.microsoft.com/mssql/server:2022-latest

# Switch to root to install fulltext - apt-get won't work unless you switch users!
USER root

# Install dependencies - these are required to make changes to apt-get below
RUN apt-get update
RUN apt-get install -yq gnupg gnupg2 gnupg1 curl apt-transport-https

# Install SQL Server package links - why aren't these already embedded in the image?  How weird.
RUN curl https://packages.microsoft.com/keys/microsoft.asc -o /var/opt/mssql/ms-key.cer
RUN apt-key add /var/opt/mssql/ms-key.cer
RUN curl https://packages.microsoft.com/config/ubuntu/20.04/mssql-server-2022.list -o /etc/apt/sources.list.d/mssql-server-2022.list
RUN apt-get update

# Install SQL Server full-text-search - this only works if you add the packages references into apt-get above
RUN apt-get install -y mssql-server-fts

# Cleanup
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists

# Run SQL Server process
ENTRYPOINT [ "/opt/mssql/bin/sqlservr" ]
