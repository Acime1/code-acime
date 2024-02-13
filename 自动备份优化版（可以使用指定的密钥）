#!/bin/bash

# 服务器A上的源目录
SRC_DIR="/root/docker/xx"

# 服务器B上的目标目录
DST_DIR="/root/docker/xx"

# 服务器B的IP地址
SERVER_B_IP="xxxxxx"

# 服务器B的SSH用户名
SSH_USER="root"

# 服务器B的SSH端口
SSH_PORT="22"

# 备份文件前缀
BACKUP_NAME_PREFIX="xxx_backup"

# 压缩文件格式
ARCHIVE_FORMAT="tar.gz"

# SSH私钥文件路径
SSH_PRIVATE_KEY="/root/.ssh/all_id_rsa_key"

# 生成备份文件名
current_date=$(date +"%Y%m%d_%H%M%S")
backup_filename="${BACKUP_NAME_PREFIX}_${current_date}.${ARCHIVE_FORMAT}"

# 压缩源目录
tar -czf "${backup_filename}" -C "${SRC_DIR}" .

# 传输备份文件到服务器B
scp -P "${SSH_PORT}" -i "${SSH_PRIVATE_KEY}" "${backup_filename}" "${SSH_USER}@${SERVER_B_IP}:${DST_DIR}"

# 删除本地备份文件
rm -f "${backup_filename}"

# 保留最多3个备份文件
ssh -p "${SSH_PORT}" -i "${SSH_PRIVATE_KEY}" "${SSH_USER}@${SERVER_B_IP}" "ls -t ${DST_DIR}/${BACKUP_NAME_PREFIX}* | tail -n +4 | xargs --no-run-if-empty rm -f"

