#!/bin/bash

dir=${1}
existingfolder="SnapDownload"
dir_current="${1}/current";
dir_downloads="${dir_current}/SnapDownload"
conf_file="${1}/current/.config/user-dirs.dirs"


if [[ ! -d ${dir} ]]; then
	echo "dir not found"
fi

if [[ ! -d "${dir_current}" ]]; then
	echo "current folder of app not found";
fi
if [[ ! -f "${conf_file}" ]]; then
	echo "config file of app not found";
fi

if [[ ! -d "$HOME/${existingfolder}" ]]; then
	echo "existing folder does not exist, creating it.."
	create=`mkdir "$HOME/${existingfolder}"`
	if [[ $create -ne 0 ]]; then
		exit 1;
	fi
else 
	echo "existingfolder basename: " `basename "$HOME/${existingfolder}"`
fi

if [[ -d "${dir_downloads}" ]]; then
	echo "removing broken link to existing folder"
	rm -Rf "${dir_downloads}";
elif [[ "${dir_downloads}" ]]; then
	rm "${dir_downloads}";
fi

echo "linking to existing folder"
ln -s "$HOME/${existingfolder}" ${dir_current}

echo "fixing user-dirs entry to link to existingfolder"
sed -i '/^XDG_DOWNLOAD_DIR/d' ${conf_file}
echo XDG_DOWNLOAD_DIR=\""\$HOME/${existingfolder}"\" >> ${conf_file}


